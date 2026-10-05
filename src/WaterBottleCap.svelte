<script>
    let {
        displayWaterGoal,
        displayWaterConsumedToday,
        sanitizationStatus
    } = $props();

    let hydrationPercentage = $derived(
        displayWaterGoal > 0
            ? Math.min(
                100,
                Math.max(
                    0,
                    (displayWaterConsumedToday / displayWaterGoal) * 100
                )
            )
            : 0
    );

    let sanitizationClass = $derived(
        sanitizationStatus === "Cleaning"
            ? "cleaning"
            : sanitizationStatus === "Clean"
                ? "clean"
                : sanitizationStatus === "Stale"
                    ? "stale"
                    : "off"
    );
    let hydrationAngle = $derived(
        (hydrationPercentage / 100) * 360 - 90
    );

    let hydrationRadians = $derived(
        hydrationAngle * Math.PI / 180
    );

    let labelRadius = 30.5;

    let labelX = $derived(
        50 + labelRadius * Math.cos(hydrationRadians)
    );

    let labelY = $derived(
        50 + labelRadius * Math.sin(hydrationRadians)
    );
</script>

<div class="bottle-cap">

    <img
        class="cap-image"
        src="/WaterBottleLidSketch.png"
        alt="Smart water bottle cap"
    />

    <!-- Outer sanitization light -->
    <div class={`sanitization-ring ${sanitizationClass}`}></div>

    <!-- Daily hydration goal -->
    <div
        class="hydration-ring"
        style={`--progress: ${hydrationPercentage * 3.6}deg`}
    ></div>

    <span
        class="hydration-percentage"
        style={`left: ${labelX}%; top: ${labelY}%`}
    >
        {Math.round(hydrationPercentage)}%
    </span>

</div>

<style>
    .bottle-cap {
        position: relative;
        width: 300px;

        container-type: inline-size;
    }

    .cap-image {
        display: block;

        width: 100%;
        height: auto;
    }

    /*
       Sanitization outer ring
    */

    .sanitization-ring {
        position: absolute;

        left: 2.5%;
        top: 1.45%;

        width: 95.4%;
        aspect-ratio: 1;

        box-sizing: border-box;

        border: 1.3cqw solid #8d8c8c;
        border-radius: 50%;

        pointer-events: none;
    }

    .sanitization-ring.cleaning {
        border-color: #facc15;

        animation: pulse 1.4s ease-in-out infinite;
    }

    .sanitization-ring.clean {
        border-color: #22c55e;

        animation: pulse 1s ease-in-out infinite;
    }

    .sanitization-ring.stale {
        border-color: #ef4444;

        animation: pulse 0.8s ease-in-out infinite;
    }

    /*
       Hydration inner ring
    */

    .hydration-ring {
        position: absolute;

        left: 11%;
        top: 10%;

        width: 78%;
        aspect-ratio: 1;

        border-radius: 50%;

        background:
            conic-gradient(
                #38bdf8 var(--progress),
                #666 0deg
            );

        -webkit-mask:
            radial-gradient(
                farthest-side,
                transparent calc(100% - 3cqw),
                #000 0
            );

        mask:
            radial-gradient(
                farthest-side,
                transparent calc(100% - 3cqw),
                #000 0
            );

        pointer-events: none;
    }

    .hydration-percentage {
        position: absolute;

        transform: translate(-50%, -50%);

        color: #38bdf8;
        font-size: 5cqw;
        font-weight: bold;

        white-space: nowrap;

        text-shadow: 0 0 4px rgba(56, 189, 248, 0.9);

        pointer-events: none;
    }

    @keyframes pulse {
        0%,
        100% {
            opacity: 0.35;
        }

        50% {
            opacity: 1;
        }
    }
</style>
