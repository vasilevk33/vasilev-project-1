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
  let phoneBatteryPercentage = $state(100);
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

  // Simulation Variables
  let isSimulating = $state(false); // Flag to indicate if simulation is running
  /** @type {ReturnType<typeof setInterval> | null} */
  let simulationInterval = null;
  let simulationTicks = 0;
  let roomTempWaterSeconds = 0; // Counter for how long the water has been at room temperature
  let staleSeconds = 0; // Counter for how long the water has been stale
  let importantSimAction = $state("Idle");

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
    powerBankChargingInterval = setInterval(() => {
      if (powerBankBatteryPercentage >= 100) {
        if (powerBankChargingInterval !== null) {
          clearInterval(powerBankChargingInterval);
          powerBankChargingInterval = null;
        }
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
    <section>
      <h2>Project Information</h2>
      <p>Project Title: Smart Water Bottle</p>
      <p>By: Kiki Vasilev</p>
      <p>Project Write Up: <a href="https://github.com/vasilevk33/vasilev-project-1/blob/main/README.md">Documentation</a></p>
      <button type="button">Info(Controls)</button>
    </section> 
    <Controls drink = {drinkWater} refill = {refillWater} stale = {staleWater} empty = {emptyWater} chargeBank = {chargePowerBank} chargeDevice = {chargeDevice} displayGoal = {displayWaterGoal} volumeUnit = {volumeUnit} toggleSimulation = {toggleSimulation} bind:unitSystem = {unitSystem} bind:waterGoal = {waterGoal} bind:cleanDuration = {cleanDuration} bind:staleDuration = {staleDuration} bind:isSimulating = {isSimulating} bind:simulationAction = {importantSimAction} />
  </div>
  <div class="right-region">
    <section class="display-section">
      <h2>Water Bottle Display</h2>
      <WaterBottleUI {displayWaterAmount} {displayWaterTemp} {displayWaterGoal} {displayWaterConsumedToday} {maxWaterCapacity} {sanitizationStatus} {powerBankBatteryPercentage} {waterIsStale} {volumeUnit} {tempUnit} {phoneBatteryPercentage}/>
      <img class="bottle-sketch" src="WaterBottleSketchNew.png" alt="Water Bottle Sketch">
      <img class="bottle-lid" src="WaterBottleLidSketch.png" alt="Water Bottle Lid Sketch">
    </section>
  </div>
</div>

<style>
  .container {
    display: flex;
    height: 100vh;
    gap: 20px;
    padding: 20px;
    box-sizing: border-box;
    width: 100%;
  }
  .left-region {
    flex: 1;
    border-right: 1px solid #ccc;
    padding-right: 20px;
  }
  .right-region {
    flex: 2;
    display: flex;
    justify-content: center;
  }
  .display-section {
    display: flex;
    flex-direction: column;
    align-items: center; 
    text-align: center;
    width: 100%;
  }
  .bottle-sketch {
    max-height: 500px;
    width: auto;
    object-fit: contain;
    margin-top: 15px;
  }
  .bottle-lid {
    max-height: 300px;
    width: auto;
    object-fit: contain;
    margin-top: 15px;
  }
</style>
