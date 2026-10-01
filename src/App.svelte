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
  let waterIsStale = $state(false);
  let unitSystem = $state("Imperial"); // Can be "Imperial" or "Metric"
  let cleanDuration = $state(5); // Duration for which the sanitization light stays green (in seconds)
  let staleDuration = $state(10); // Duration for which the sanitization light stays red (in seconds)

  // Functions
  function drinkWater() {
    if (waterIsStale) {
      sanitizationStatus = "Stale"; // Red Light
      setTimeout(() => {
        sanitizationStatus = "Off"; // Off when red light finishes
      }, staleDuration * 1000); // convert seconds to milliseconds
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
      waterIsStale = false;
      cleanWater();
    }
    function cleanWater() {
      sanitizationStatus = "Cleaning"; // Yellow Light for 10 seconds (assume cleaning time is always 10 seconds)
      setTimeout(() => {
        sanitizationStatus = "Clean"; // Green Light
        waterIsStale = false;
      }, 10000);
      setTimeout(() => {
        sanitizationStatus = "Off"; // Off when green light finishes
      }, 10000 + (cleanDuration * 1000)); // convert seconds to milliseconds
    }
    function staleWater() {
      if (waterAmount === 0) {
        return; // No water to make stale
      }
      waterIsStale = true;
      sanitizationStatus = "Stale"; // Red Light
      setTimeout(() => {
        sanitizationStatus = "Off"; // Off when red light finishes
      }, staleDuration * 1000); // convert seconds to milliseconds
    }
    function emptyWater() {
      waterAmount = 0;
      waterIsStale = false;
      sanitizationStatus = "Off"; // Off when no water left in bottle
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
    <Controls drink = {drinkWater} refill = {refillWater} stale = {staleWater} empty = {emptyWater} chargeBank = {chargePowerBank} chargeDevice = {chargeDevice} displayGoal = {displayWaterGoal} volumeUnit = {volumeUnit} bind:unitSystem = {unitSystem} bind:waterGoal = {waterGoal} bind:cleanDuration = {cleanDuration} bind:staleDuration = {staleDuration} />
  </div>
  <div class="right-region">
    <section class="display-section">
      <h2>Water Bottle Display</h2>
      <WaterBottleUI {displayWaterAmount} {displayWaterTemp} {displayWaterGoal} {displayWaterConsumedToday} {maxWaterCapacity} {sanitizationStatus} {powerBankBatteryPercentage} {waterIsStale} {volumeUnit} {tempUnit}/>
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
