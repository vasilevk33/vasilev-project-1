<script>
  import WaterBottleUI from './WaterBottleUI.svelte';
  import Controls from './Controls.svelte';

  // State variables for the water bottle
  let waterAmount = $state(40); // in ounces
  let waterTemp = $state(50); // in Fahrenheit
  let waterGoal = $state(100); // in ounces
  let waterConsumedToday = $state(0);
  let maxWaterCapacity = $state(40); // in ounces
  let sanitizationStatus = $state("Off"); // Can be "Off", "Cleaning", "Clean", "Stale"
  let powerBankBatteryPercentage = $state(100);
  let phoneBatteryPercentage = $state(50);
  /** @type {ReturnType<typeof setInterval> | null} */
  let deviceChargingInterval = null;
  /** @type {ReturnType<typeof setInterval> | null} */
  let powerBankChargingInterval = null;
  let waterIsStale = $state(false);
  let unitSystem = $state("Imperial"); // Can be "Imperial" or "Metric"
  let cleanDuration = $state(5); // Duration for which the sanitization light stays green (in seconds)
  let staleDuration = $state(10); // Duration for which the sanitization light stays red (in seconds)
  /** @type {ReturnType<typeof setInterval> | null} */
  let activeAlertTimer = null;
  let isPowerBankCharging = $state(false);

  // Simulation Variables
  let isSimulating = $state(false); // Flag to indicate if simulation is running
  /** @type {ReturnType<typeof setInterval> | null} */
  let simulationInterval = null;
  let simulationTicks = 0;
  let roomTempWaterSeconds = 0; // Counter for how long the water has been at room temperature
  let staleSeconds = 0; // Counter for how long the water has been stale
  let importantSimAction = $state("Idle");

  // Modal State
  let showInfoModal = $state(false);

  // Functions
  function drinkWater() {
    if (sanitizationStatus === "Cleaning") {
      return; // Prevent drinking while cleaning
    }
    if (waterIsStale) {
      clearAlertTimer(); // Stops any stale timers from turning off the light early
      sanitizationStatus = "Stale"; // Red Light

      activeAlertTimer = setTimeout(() => {
        sanitizationStatus = "Off"; // Off when red light finishes
      }, staleDuration * 1000); // convert seconds to milliseconds
      return;
    }
    if (waterAmount >= 2) {
      waterAmount -= 2;
      waterConsumedToday += 2;
    }
    else if (waterAmount > 0) {
      waterConsumedToday += waterAmount;
      waterAmount = 0;
    }
  }

  function refillWater() {
    if (waterAmount === maxWaterCapacity) {
      return; // Already full
    }
    waterAmount = maxWaterCapacity;
    waterTemp = 55; // In Fahrenheit
    waterIsStale = false;
    roomTempWaterSeconds = 0; // For simulation
    cleanWater();
  }

  function cleanWater() {
    clearAlertTimer(); // Stops timers from turning off the light early
    sanitizationStatus = "Cleaning"; // Yellow Light for 10 seconds (assume cleaning time is always 10 seconds)

    // Timer for cleaning duration (10 seconds) before turning green
    activeAlertTimer = setTimeout(() => {
      sanitizationStatus = "Clean"; // Green Light
      waterIsStale = false;
      
      // Timer for green light duration (cleanDuration) before turning off
      activeAlertTimer = setTimeout(() => {
        sanitizationStatus = "Off"; // Off when green light finishes
      }, cleanDuration * 1000); // convert seconds to milliseconds
    }, 10000);
  }

  function staleWater() {
    if (waterAmount === 0) {
      return; // No water to make stale
    }
    clearAlertTimer(); // Stops timers from turning off the light early
    waterIsStale = true;
    sanitizationStatus = "Stale"; // Red Light

    activeAlertTimer = setTimeout(() => {
      sanitizationStatus = "Off"; // Off when red light finishes
    }, staleDuration * 1000); // convert seconds to milliseconds
  }

  function emptyWater() {
    clearAlertTimer(); // Stops timers from turning off the light early
    waterAmount = 0;
    waterIsStale = false;
    sanitizationStatus = "Off"; // Off when no water left in bottle
  }

  // Function to clear any active timers that might be running
  function clearAlertTimer() {
    if (activeAlertTimer !== null) {
      clearTimeout(activeAlertTimer);
      activeAlertTimer = null;
    }
  }

  function chargePowerBank() {
    if (powerBankChargingInterval !== null) {
      return;
    }
    isPowerBankCharging = true;
    powerBankChargingInterval = setInterval(() => {
      if (powerBankBatteryPercentage >= 100) {
        if (powerBankChargingInterval !== null) {
          clearInterval(powerBankChargingInterval);
          powerBankChargingInterval = null;
        }
        isPowerBankCharging = false;
        return;
      }
      powerBankBatteryPercentage = Math.min( powerBankBatteryPercentage + 10, 100);
    }, 500); // Charge power bank 10% every 1/2 of a second
  }

  function chargeDevice() {
    if (deviceChargingInterval !== null) {
      return;
    }
    deviceChargingInterval = setInterval(() => {
      if (phoneBatteryPercentage >= 100 || powerBankBatteryPercentage <= 0) {
        if (deviceChargingInterval !== null) {
          clearInterval(deviceChargingInterval);
          deviceChargingInterval = null;
        }
        return;
      }
      const chargeAmount = Math.min(10, powerBankBatteryPercentage, 100 - phoneBatteryPercentage); // charge either 10%, whatever left in powerbank, or whatever is needed to reach 100% on the phone
      phoneBatteryPercentage += chargeAmount;
      powerBankBatteryPercentage -= chargeAmount;
    }, 2000); // Charge device 10% every 2 seconds, and decrease power bank by 10% every 2 seconds
  }

  // Display units based on the selected unit system
  let displayWaterAmount = $derived(
    unitSystem === "Imperial" ? Math.round(waterAmount): Math.round(waterAmount * 29.5735));
  let displayWaterGoal = $derived(
    unitSystem === "Imperial" ? Math.round(waterGoal): Math.round(waterGoal * 29.5735));
  let displayWaterConsumedToday = $derived(
    unitSystem === "Imperial" ? Math.round(waterConsumedToday): Math.round(waterConsumedToday * 29.5735));
  let displayMaxWaterCapacity = $derived(
    unitSystem === "Imperial" ? Math.round(maxWaterCapacity): Math.round(maxWaterCapacity * 29.5735));
  let displayWaterTemp = $derived(
    unitSystem === "Imperial" ? Math.round(waterTemp): Math.round((waterTemp - 32) * 5/9));
  let volumeUnit = $derived(unitSystem === "Imperial" ? "oz" : "ml");
  let tempUnit = $derived(unitSystem === "Imperial" ? "°F" : "°C");

  function toggleSimulation() {
    isSimulating = !isSimulating;
    if (isSimulating) {
      importantSimAction = "Nothing Yet ...";
      simulationInterval = setInterval(() => {
        simulationTicks += 1;
        if (waterAmount > 0 && waterTemp < 70) {
          waterTemp += 0.5; // Increase water temp by every half second until it hits room temp (70°F)
        }
        if (phoneBatteryPercentage > 0 && deviceChargingInterval === null) {
          phoneBatteryPercentage -= 1; // Decrease phone battery by 1% every second
        }
        if (simulationTicks % 4 === 0 && powerBankBatteryPercentage > 0) {
          powerBankBatteryPercentage -= 1; // Decrease power bank battery by 1% every 4 seconds
        }
        if (waterAmount > 0 && waterTemp >= 70 && !waterIsStale) {
          roomTempWaterSeconds += 1; // Increment the counter for how long the water has been at room temp
          if (roomTempWaterSeconds >= 10) {
            staleWater(); // Make water stale after 10 seconds at room temp
            roomTempWaterSeconds = 0;
          }
        } else {
          roomTempWaterSeconds = 0; // Reset if water refilled or emptied
        }
        if (simulationTicks % 2 === 0) {
          if (waterAmount > 0) {
            drinkWater(); // Drink water every 2 seconds
          }
        }
        if (waterAmount === 0) {
          importantSimAction = "Refilled water!";
          refillWater(); // Refill water when empty
        }
        if (waterIsStale) {
          staleSeconds += 1; // Increment the counter for how long the water has been stale
          if (staleSeconds >= staleDuration) {
            importantSimAction = "Emptied stale water!";
            emptyWater(); // Empty water when stale duration is reached
          }
        } else {
          staleSeconds = 0; // Reset if water is no longer stale
        }
        if (phoneBatteryPercentage === 20) {
          importantSimAction = "Charging device...";
          chargeDevice(); // Charge device when phone battery is low (20%)
        }
        if (powerBankBatteryPercentage === 0) {
          importantSimAction = "Charging power bank...";
          chargePowerBank(); // Charge power bank when battery is 0%
        }
        if (waterConsumedToday >= waterGoal) {
          importantSimAction = "Goal reached!";
          // Stop the simulation
          if (simulationInterval !== null) {
            clearInterval(simulationInterval);
            simulationInterval = null;
          }
          isSimulating = false;
        }
      }, 1000);
    } else {
      importantSimAction = "Paused";
      // Stop the simulation
      if (simulationInterval !== null) {
        clearInterval(simulationInterval);
        simulationInterval = null;
      }
    }
  }
</script>

<div class="container">
  <div class="left-region">
    <section class="project-info-card">
      <h2>Project Information</h2>
      <p><strong>Project Title:</strong> Smart Water Bottle</p>
      <p><strong>By:</strong> Kiki Vasilev</p>
      <p><strong>Project Write Up:</strong> <a href="https://github.com/vasilevk33/vasilev-project-1/blob/main/README.md" target="_blank" rel="noreferrer">Documentation</a></p>
      <button class="info-btn" type="button" onclick={() => showInfoModal = true}>
        ℹ️ Info (Controls Guide)
      </button>
    </section> 

    <Controls 
      drink={drinkWater} 
      refill={refillWater} 
      stale={staleWater} 
      empty={emptyWater} 
      chargeBank={chargePowerBank} 
      chargeDevice={chargeDevice} 
      displayGoal={displayWaterGoal} 
      volumeUnit={volumeUnit} 
      toggleSimulation={toggleSimulation} 
      bind:unitSystem={unitSystem} 
      bind:waterGoal={waterGoal} 
      bind:cleanDuration={cleanDuration} 
      bind:staleDuration={staleDuration} 
      bind:isSimulating={isSimulating} 
      bind:simulationAction={importantSimAction} 
    />
  </div>

  <div class="right-region">
    <section class="display-section">
      <h2>Smart Water Bottle Interface</h2>
      <WaterBottleUI 
        {displayWaterAmount} 
        {displayWaterTemp} 
        {displayWaterGoal} 
        {displayWaterConsumedToday} 
        {displayMaxWaterCapacity} 
        {sanitizationStatus} 
        {powerBankBatteryPercentage} 
        {volumeUnit} 
        {tempUnit} 
        {phoneBatteryPercentage} 
        {isPowerBankCharging} 
        bind:unitSystem={unitSystem} 
        bind:waterGoal={waterGoal} 
        bind:cleanDuration={cleanDuration} 
        bind:staleDuration={staleDuration}
      />
    </section>
  </div>
</div>

{#if showInfoModal}
  <!-- Backdrop (click outside to close) -->
  <div
    class="modal-backdrop"
    role="presentation"
    onclick={(event) => {
      if (event.target === event.currentTarget) {
        showInfoModal = false;
      }
    }}
  >
    <!-- Modal Card (stop propagation so clicking inside doesn't close) -->
    <div class="modal-card" role="dialog" aria-modal="true">
      <div class="modal-header">
        <h3>Smart Water Bottle Controls & Features</h3>
        <button class="close-btn" type="button" onclick={() => showInfoModal = false} aria-label="Close modal">✕</button>
      </div>

      <div class="modal-body">
        <div class="guide-item">
          <h4>💧 Hydration</h4>
          <p><strong>Body Water Level:</strong> Displays water height and real-time remaining percentage along the bottle body.</p>
          <p><strong>Cap Hydration Ring:</strong> Circular progress ring indicating percent progress toward your daily water goal.</p>
          <p><strong>Manual Sips, Refill & Emptying:</strong> "Drink" takes 2 oz (60 ml) sips; "Refill Water" restores maximum capacity (40 oz / 1183 ml); "Empty Water" drains all water from the bottle (0 oz / 0 ml).</p>
        </div>

        <div class="guide-item">
          <h4>🧪 Sanitization Alerts</h4>
          <p><strong>Lid LED Ring:</strong> Flashes Yellow 🟡 during active cleaning (10s), Green 🟢 when sanitization completes successfully, Red 🔴 when water is stale, off otherwise.</p>
          <p><strong>Cleaning Logic:</strong> Every time water is refilled, the bottle initiates a cleaning cycle.</p>
          <p><strong>Stale Water Logic:</strong> If water rests at or above 70°F for 10 continuous seconds it enters a stale state.</p>
          <p><strong>Manual Stale Button:</strong> "Make Water Stale" makes the water stale immediately.</p>
        </div>

        <div class="guide-item">
          <h4>🔋 Power Bank</h4>
          <p><strong>Detachable Base:</strong> Features a rechargeable battery bank powering both water bottle sensors and external devices.</p>
          <p><strong>Device Charging:</strong> "Charge External Device" transfers battery from the base to your connected phone. "Charge Power Bank" charges the base to 100%.</p>
        </div>

        <div class="guide-item">
          <h4>📱 Phone App</h4>
          <p><strong>Bottle Information:</strong> Displays water remaining, hydration-goal progress, phone battery level, and connection status.</p>
          <p><strong>Interactive Settings:</strong> Customize your daily water goal (80–180 oz), switch between Imperial and Metric units, and adjust how long Green and Red alert lights remain active (1-30 seconds).</p>
        </div>

        <div class="guide-item">
          <h4>⏱️ Live Simulation Mode</h4>
          <p>Runs an autonomous simulation that warms water toward room temperature (70°F), simulates periodic drinking (every 2 seconds), auto-discards stale water, auto refills water, and charges low batteries.</p>
        </div>
      </div>
    </div>
  </div>
{/if}

<style>
  :global(body) {
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    background-color: #fafafa;
    color: #222;
  }

  .container {
    display: flex;
    min-height: 100vh;
    box-sizing: border-box;
    width: 100%;
  }

  .left-region {
    flex: 0 0 320px;
    background: #ffffff;
    border-right: 1px solid #e0e0e0;
    padding: 24px;
    box-sizing: border-box;
    overflow-y: auto;
    height: 100vh;
  }

  .right-region {
    flex: 1;
    padding: 24px;
    box-sizing: border-box;
    overflow-y: auto;
    height: 100vh;
    display: flex;
    justify-content: center;
  }

  .project-info-card {
    margin-bottom: 20px;
    padding-bottom: 16px;
    border-bottom: 1px solid #eee;
  }

  .project-info-card h2 {
    margin-top: 0;
    margin-bottom: 10px;
    font-size: 20px;
  }

  .project-info-card p {
    margin: 6px 0;
    font-size: 14px;
    color: #444;
  }

  .project-info-card a {
    color: #0284c7;
    text-decoration: none;
    font-weight: 500;
  }

  .project-info-card a:hover {
    text-decoration: underline;
  }

  .info-btn {
    width: 100%;
    margin-top: 10px;
    padding: 8px 12px;
    background: #f0fdf4;
    border: 1px solid #86efac;
    color: #166534;
    border-radius: 6px;
    font-weight: 600;
    font-size: 13px;
    cursor: pointer;
    transition: background 0.2s;
  }

  .info-btn:hover {
    background: #dcfce7;
  }

  .display-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    max-width: 1200px;
  }

  .display-section h2 {
    margin-top: 0;
    margin-bottom: 20px;
  }

  /* Modal Overlay Styling */
  .modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.45);
    backdrop-filter: blur(2px);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
  }

  .modal-card {
    background: #ffffff;
    width: 90%;
    max-width: 580px;
    max-height: 85vh;
    border-radius: 14px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
    overflow: hidden;
    animation: popIn 0.2s ease-out;
  }

  @keyframes popIn {
    from {
      opacity: 0;
      transform: scale(0.95);
    }
    to {
      opacity: 1;
      transform: scale(1);
    }
  }

  .modal-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px 20px;
    border-bottom: 1px solid #e5e7eb;
    background: #f9fafb;
  }

  .modal-header h3 {
    margin: 0;
    font-size: 17px;
    color: #111827;
  }

  .close-btn {
    background: transparent;
    border: none;
    font-size: 18px;
    font-weight: bold;
    color: #6b7280;
    cursor: pointer;
    border-radius: 6px;
    padding: 4px 8px;
    line-height: 1;
  }

  .close-btn:hover {
    background: #e5e7eb;
    color: #111827;
  }

  .modal-body {
    padding: 20px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .guide-item h4 {
    margin: 0 0 6px 0;
    font-size: 15px;
    color: #0f172a;
  }

  .guide-item p {
    margin: 4px 0;
    font-size: 13.5px;
    line-height: 1.5;
    color: #4b5563;
  }
</style>
