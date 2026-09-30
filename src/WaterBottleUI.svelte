<script>
    let { waterAmount, waterTemp, waterGoal, waterConsumedToday, maxWaterCapacity, sanitizationStatus, powerBankBatteryPercentage, waterIsStale } = $props();
</script>

<p>Water Amount Remaining: {waterAmount} oz</p>
<p>Water Temperature: {waterTemp}°F</p>
<p>Daily Goal: {waterConsumedToday} oz / {waterGoal} oz</p>
<p>Sanitization Light: {sanitizationStatus}</p>
<p>Power Bank Battery: {powerBankBatteryPercentage}%</p>
