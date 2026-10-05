<script>
    let {
        displayWaterAmount,
        displayWaterGoal,
        displayWaterConsumedToday,
        volumeUnit,
        phoneBatteryPercentage,

        unitSystem = $bindable("Imperial"),
        waterGoal = $bindable(100),
        cleanDuration = $bindable(5),
        staleDuration = $bindable(10)
    } = $props();
</script>

<div class="phone">

    <div class="phone-top">
        <div class="speaker"></div>

        <div class="status-icons">
            <span class="bluetooth">ᛒ</span>

            <div class="battery">
                <div
                    class="battery-fill"
                    style={`width: ${phoneBatteryPercentage}%`}
                ></div>

                <span>
                    {Math.round(phoneBatteryPercentage)}%
                </span>
            </div>
        </div>
    </div>

    <div class="phone-content">

        <h2>Smart Water Bottle</h2>

        <p class="connected">
            Water Bottle Connected
        </p>

        <div class="info-row">
            <span>Water Remaining</span>

            <strong>
                {displayWaterAmount} {volumeUnit}
            </strong>
        </div>

        <div class="info-row">
            <span>Daily Goal Progress</span>

            <strong>
                {displayWaterConsumedToday} {volumeUnit}
                /
                {displayWaterGoal} {volumeUnit}
            </strong>
        </div>

        <div class="setting">
            <label>
                Daily Goal

                <strong>
                    {displayWaterGoal} {volumeUnit}
                </strong>
            </label>

            <input
                type="range"
                min="80"
                max="180"
                step="2"
                bind:value={waterGoal}
            />
        </div>

        <div class="setting">
            <p>Select Units</p>

            <label class="radio-option">
                <input
                    type="radio"
                    bind:group={unitSystem}
                    value="Imperial"
                />

                Imperial
            </label>

            <label class="radio-option">
                <input
                    type="radio"
                    bind:group={unitSystem}
                    value="Metric"
                />

                Metric
            </label>
        </div>

        <div class="setting">
            <label>
                Clean Alert Duration

                <strong>
                    {cleanDuration}s
                </strong>
            </label>

            <input
                type="range"
                min="1"
                max="30"
                step="1"
                bind:value={cleanDuration}
            />
        </div>

        <div class="setting">
            <label>
                Stale Alert Duration

                <strong>
                    {staleDuration}s
                </strong>
            </label>

            <input
                type="range"
                min="1"
                max="30"
                step="1"
                bind:value={staleDuration}
            />
        </div>

    </div>

    <div class="home-indicator"></div>

</div>

<style>
    .phone {
        position: relative;

        width: 310px;
        height: 700px;

        box-sizing: border-box;

        padding: 22px 24px 32px;

        border: 8px solid #282828;
        border-radius: 42px;

        background: #f7f8f3;

        container-type: inline-size;
    }

    .phone-top {
        position: relative;
        height: 38px;
    }

    .speaker {
        position: absolute;

        left: 50%;
        top: -7px;

        transform: translateX(-50%);

        width: 34%;
        height: 20px;

        border-radius: 20px;

        background: #282828;
    }

    .status-icons {
        position: absolute;

        right: 0;
        top: 0;

        display: flex;
        align-items: center;
        gap: 7px;
    }

    .bluetooth {
        font-size: 17px;
        font-weight: bold;
    }

    .battery {
        position: relative;

        width: 45px;
        height: 18px;

        box-sizing: border-box;

        border: 2px solid #060606;
        border-radius: 4px;

        background: #555;

        overflow: visible;
    }

    .battery::before {
        content: "";

        position: absolute;

        right: -6%;
        top: 30%;

        width: 6%;
        height: 40%;

        background: #060606;

        border-radius: 0 2px 2px 0;
    }

    .battery-fill {
        position: absolute;

        left: 0;
        top: 0;

        height: 100%;

        background: #13b950;

        border-radius: 2px;

        transition: width 0.4s ease;
    }

    .battery span {
        position: absolute;

        left: 50%;
        top: 50%;

        transform: translate(-50%, -50%);

        color: white;

        font-size: 8px;
        font-weight: bold;

        z-index: 1;
    }

    .phone-content {
        margin-top: 5px;
    }

    .small-title {
        margin: 0;

        font-size: 10px;
        letter-spacing: 2px;
    }

    h2 {
        margin: 6px 0 3px;

        font-size: 24px;
    }

    .connected {
        margin: 0 0 16px;

        font-size: 12px;
    }

    .info-row {
        display: flex;
        justify-content: space-between;
        gap: 10px;

        padding: 10px 0;

        border-bottom: 1px solid #ddd;

        font-size: 13px;
    }

    .info-row strong {
        text-align: right;
    }

    .setting {
        margin-top: 14px;
    }

    .setting > label {
        display: flex;
        justify-content: space-between;

        font-size: 13px;
    }

    .setting input[type="range"] {
        width: 100%;

        margin-top: 5px;
    }

    .setting p {
        margin: 0 0 5px;

        font-size: 13px;
    }

    .radio-option {
        display: inline-flex;
        align-items: center;

        margin-right: 10px;

        font-size: 13px;
    }

    .home-indicator {
        position: absolute;

        left: 50%;
        bottom: 10px;

        transform: translateX(-50%);

        width: 38%;
        height: 5px;

        border-radius: 10px;

        background: #282828;
    }
</style>