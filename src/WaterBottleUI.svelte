<script>
    let { waterAmount, waterTemp = $bindable(), waterGoal, waterConsumedToday, userPreferedTemp } = $props();

    function increaseWaterTemp() {
        waterTemp += 1;
    }
    function decreaseWaterTemp() {
        waterTemp -= 1;
    }
    function coldTempPreset() {
        waterTemp = 40;
    }
    function roomTempPreset() {
        waterTemp = 70;
    }
    function favoriteTempPreset() {
        waterTemp = userPreferedTemp;
    }
</script>

<p>Water Amount Remaining: {waterAmount} oz</p>
<p>Water Temperature: {waterTemp}°F</p>
<p>Daily Goal: {waterConsumedToday} oz / {waterGoal} oz</p>

<p>Adjust Water Temperature:</p>
<button onclick={increaseWaterTemp}>
	+
</button>
<button onclick={decreaseWaterTemp}>
	-
</button>

<p>Temperature Presets:</p>
<button onclick={coldTempPreset}>
	Cold (40°F)
</button>
<button onclick={roomTempPreset}>
	Room (70°F)
</button>
<button onclick={favoriteTempPreset}>
	Favorite Temp! ({userPreferedTemp}°F)
</button>
