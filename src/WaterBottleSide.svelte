<script>
    let {
        displayWaterAmount,
        displayWaterTemp,
        displayMaxWaterCapacity,
        volumeUnit,
        tempUnit,
        powerBankBatteryPercentage,
        isPowerBankCharging
    } = $props();

    let waterPercentage = $derived(
        Math.min(
            100,
            Math.max(0, (displayWaterAmount / displayMaxWaterCapacity) * 100)
        )
    );
</script>

<div class="bottle-side">

    <!-- Bottle drawing -->
    <img
        class="bottle-image"
        src="/WaterBottleSketchNew.png"
        alt="Smart water bottle"
    />

    <!-- Water level indicator -->
    <div class="water-track">

        <div
            class="water-fill"
            style={`height: ${waterPercentage}%`}
        >
            <span>{Math.round(waterPercentage)}%</span>
        </div>

    </div>

    <!-- Water temperature -->
    <div class="temperature-display">
        {displayWaterTemp}{tempUnit}
    </div>

    <div class="battery" class:charging={isPowerBankCharging}>
        <div
            class="battery-fill"
            style={`height: ${powerBankBatteryPercentage}%`}
        ></div>

        <span>
            {Math.round(powerBankBatteryPercentage)}%
        </span>
    </div>

</div>

<style>
    .bottle-side {
        position: relative;
        width: 240px;
        container-type: inline-size;
    }

    .bottle-image {
        display: block;
        width: 100%;
        height: auto;
    }

    /*
     * Invisible area representing the bottle's water-level sensor.
     */
    .water-track {
        position: absolute;

        left: 25%;
        top: 25.3%;
        bottom: 13.96%;

        width: 6%;

        pointer-events: none;
    }

    /*
     * The actual blue water level.
     */
    .water-fill {
        position: absolute;

        left: 0;
        bottom: 0;

        width: 100%;

        background: #38bdf8;

        border-radius: 20px;

        box-shadow:
            0 0 8px #38bdf8,
            0 0 16px #38bdf8;

        transition: height 0.5s ease;
    }

    /*
     * Percentage stays at the top of the
     * currently filled water level.
     */
    .water-fill span {
        position: absolute;

        right: -36px;
        top: 0;

        transform: translateY(-50%);

        color: #38bdf8;

        font-size: 5.5cqw;
        font-weight: bold;

        white-space: nowrap;

        text-shadow: 0 0 8px #38bdf8;
    }

    /*
     * Temperature display on the bottle.
     */
    .temperature-display {
        position: absolute;

        left: 52%;
        top: 30%;

        width: 33.7%;
        height: 6.5%;

        box-sizing: border-box;

        display: flex;
        align-items: center;
        justify-content: center;

        border-radius: 6px;

        background: #292929;

        border: 2px solid #555;

        color: #f5f5f5;

        font-family: "Courier New", monospace;
        font-size: 9cqw;
        font-weight: bold;

        letter-spacing: 0.15cqw;

        white-space: nowrap;

        box-shadow:
            inset 0 0 5px rgba(0, 0, 0, 0.8);
    }
    .battery {
        position: absolute;

        left: 64%;
        bottom: 2.5%;

        width: 12%;
        height: 7%;

        box-sizing: border-box;

        border: 2px solid #060606;
        border-radius: 4px;

        background: #555;

        overflow: visible;

        pointer-events: none;
    }

    .battery-fill {
        position: absolute;

        left: 0;
        bottom: 0;

        width: 100%;

        background: #13b950;

        transition: height 0.4s ease;
        border-radius: 1cqw 1cqw 1cqw 1cqw;
    }

    .battery span {
        position: absolute;

        left: 50%;
        top: 50%;

        transform: translate(-50%, -50%);

        color: rgb(17, 122, 29);

        font-size: 4cqw;
        font-weight: bold;

        z-index: 1;
    }
    .battery::before {
        content: "";

        position: absolute;

        top: -9%;
        left: 35%;

        width: 30%;
        height: 10%;

        background: #060606;

        border-radius: 2px 2px 0 0;
    }
    .battery.charging .battery-fill {
        animation: charging-pulse 1s ease-in-out infinite;
        box-shadow: 0 0 8px #22c55e;
    }

    @keyframes charging-pulse {
        0%,
        100% {
            opacity: 0.55;
        }

        50% {
            opacity: 1;
        }
    }
</style>
