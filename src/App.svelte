<script>
  import WaterBottleUI from './WaterBottleUI.svelte';
  import Controls from './Controls.svelte';

  // State variables for the water bottle
  let waterAmount = $state(40); // in ounces
  let waterTemp = $state(50); // in Fahrenheit
  let waterGoal = 100;
  let waterConsumedToday = $state(0);
  let maxWaterCapacity = 40; // in ounces
  let sanitizationStatus = $state("Off"); // Can be "Off", "Cleaning", "Clean", "Stale"
  let powerBankBatteryPercentage = $state(100);
  let waterIsStale = $state(false);

  // Functions
  function drinkWater() {
        if (waterIsStale) {
            sanitizationStatus = "Stale"; // Red Light for 5 seconds
            setTimeout(() => {
                sanitizationStatus = "Off"; // Off when red light finishes
            }, 5000);
            return;
        }
        if (sanitizationStatus === "Cleaning") {
          return; // Prevent drinking while cleaning
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
        waterTemp = 60; // In Fahrenheit
        cleanWater();
    }
    function cleanWater() {
        sanitizationStatus = "Cleaning"; // Yellow Light for 10 seconds
        setTimeout(() => {
            sanitizationStatus = "Clean"; // Green Light for 5 seconds
            waterIsStale = false;
        }, 10000);
        setTimeout(() => {
            sanitizationStatus = "Off"; // Off when green light finishes
        }, 15000);
    }
    function staleWater() {
        waterIsStale = true;
        sanitizationStatus = "Stale"; // Red Light for 10 seconds
        setTimeout(() => {
            sanitizationStatus = "Off"; // Off when red light finishes
        }, 10000);
    }
    function chargePowerBank() {
        powerBankBatteryPercentage = 100;
    }
    function chargeDevice() {
        if (powerBankBatteryPercentage >= 10) {
            powerBankBatteryPercentage -= 10;
        }
        else if (powerBankBatteryPercentage > 0) {
            powerBankBatteryPercentage = 0;
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
    <Controls drink = {drinkWater} refill = {refillWater} stale = {staleWater} chargeBank = {chargePowerBank} chargeDevice = {chargeDevice} />
  </div>
  <div class="right-region">
    <section class="display-section">
      <h2>Water Bottle Display</h2>
      <WaterBottleUI {waterAmount} {waterTemp} {waterGoal} {waterConsumedToday} {maxWaterCapacity} {sanitizationStatus} {powerBankBatteryPercentage} {waterIsStale}/>
      <img class="bottle-sketch" src="WaterBottleSketch.png" alt="Water Bottle Sketch">
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
</style>
