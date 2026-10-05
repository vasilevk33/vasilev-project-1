<script>
    import WaterBottleSide from "./WaterBottleSide.svelte";
    import WaterBottleCap from "./WaterBottleCap.svelte";
    import PhoneUI from "./PhoneUI.svelte";

    let {
        displayWaterAmount,
        displayWaterTemp,
        displayWaterGoal,
        displayWaterConsumedToday,
        displayMaxWaterCapacity,
        sanitizationStatus,
        powerBankBatteryPercentage,
        waterIsStale,
        volumeUnit,
        tempUnit,
        phoneBatteryPercentage,
        isPowerBankCharging,

        unitSystem = $bindable("Imperial"),
        waterGoal = $bindable(100),
        cleanDuration = $bindable(5),
        staleDuration = $bindable(10)
    } = $props();
</script>

<WaterBottleSide
    {displayWaterAmount}
    {displayWaterTemp}
    {displayMaxWaterCapacity}
    {volumeUnit}
    {tempUnit}
    {powerBankBatteryPercentage}
    {isPowerBankCharging}
/>

<WaterBottleCap
    {displayWaterGoal}
    {displayWaterConsumedToday}
    {sanitizationStatus}
/>

<PhoneUI
    {displayWaterAmount}
    {displayWaterGoal}
    {displayWaterConsumedToday}
    {volumeUnit}
    {phoneBatteryPercentage}
    bind:unitSystem
    bind:waterGoal
    bind:cleanDuration
    bind:staleDuration
/>
