<script>
    let { displayWaterAmount, displayWaterTemp, displayWaterGoal, displayWaterConsumedToday, maxWaterCapacity, sanitizationStatus, powerBankBatteryPercentage, waterIsStale, volumeUnit, tempUnit, phoneBatteryPercentage } = $props();
</script>

<p>Water Amount Remaining: {displayWaterAmount} {volumeUnit}</p>
<p>Water Temperature: {displayWaterTemp} {tempUnit}</p>
<p>Daily Goal: {displayWaterConsumedToday} {volumeUnit} / {displayWaterGoal} {volumeUnit}</p>
<p>Sanitization Light: {sanitizationStatus}</p>
<p>Power Bank Battery: {powerBankBatteryPercentage}%</p>
<p>Phone Battery: {phoneBatteryPercentage}%</p>
