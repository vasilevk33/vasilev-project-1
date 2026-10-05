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

<div class="bottle-ui-layout">
    <!-- View 1: Bottle Front Card -->
    <div class="view-card">
        <h3>Bottle Front View</h3>
        <div class="component-wrapper">
            <WaterBottleSide
                {displayWaterAmount}
                {displayWaterTemp}
                {displayMaxWaterCapacity}
                {volumeUnit}
                {tempUnit}
                {powerBankBatteryPercentage}
                {isPowerBankCharging}
            />
        </div>
    </div>

    <!-- View 2: Bottle Top Card -->
    <div class="view-card">
        <h3>Bottle Top View</h3>
        <div class="component-wrapper">
            <WaterBottleCap
                {displayWaterGoal}
                {displayWaterConsumedToday}
                {sanitizationStatus}
            />
        </div>
    </div>

    <!-- View 3: Phone App Card -->
    <div class="view-card">
        <h3>Phone App</h3>
        <div class="component-wrapper">
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
        </div>
    </div>
</div>

<style>
    .bottle-ui-layout {
        display: flex;
        flex-direction: row;
        align-items: stretch;
        justify-content: center;
        gap: 16px;
        width: 100%;
        box-sizing: border-box;
    }

    /* ard frame */
    .view-card {
        flex: 1;
        min-width: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        background: #ffffff;
        border: 1px solid #e5e7eb;
        border-radius: 12px;
        padding: 16px 12px;
        box-shadow: 0 1px 3px rgba(0, 0, 0, 0.04);
        box-sizing: border-box;
    }

    .view-card h3 {
        margin: 0 0 12px 0;
        font-size: 14px;
        font-weight: 600;
        letter-spacing: 0.05em;
        text-transform: uppercase;
        color: #4b5563;
    }

    .component-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
    }
</style>
