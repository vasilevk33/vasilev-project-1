<script>
    let { drink, refill, stale, empty, chargeBank, chargeDevice, displayGoal, volumeUnit, toggleSimulation, isSimulating = $bindable(false),
    unitSystem = $bindable("Imperial"), waterGoal = $bindable(100), cleanDuration = $bindable(5), staleDuration = $bindable(10) 
    } = $props();
</script>

<h2>Test Controls</h2>
<button onclick={drink}>Drink ({unitSystem === "Imperial" ? "2 oz" : "60 ml"})</button>
<button onclick={refill}>Refill Water</button>
<button onclick={stale}>Make Water Stale</button>
<button onclick={empty}>Empty Water</button>
<button onclick={chargeBank}>Charge Power Bank (100%)</button>
<button onclick={chargeDevice}>Charge External Device</button>
<button onclick={toggleSimulation}>
  {isSimulating ? "Pause Simulation" : "Start Simulation"}
</button>
<h2>Phone Controls</h2>
<label> Daily Goal: {displayGoal} {volumeUnit}
<input type="range" min="80" max="180" step="2" bind:value={waterGoal} />
</label>
<label>
  <input type="radio" bind:group={unitSystem} value="Imperial" />
  Imperial
</label>
<label>
  <input type="radio" bind:group={unitSystem} value="Metric" />
  Metric
</label>
  
<label>
Clean Alert (Green Light): {cleanDuration}s
<input 
    type="range" 
    min="1" 
    max="30" 
    step="1" 
    bind:value={cleanDuration} 
/>
</label>

<label>
Stale Alert (Red Light): {staleDuration}s
<input 
    type="range" 
    min="1" 
    max="30" 
    step="1" 
    bind:value={staleDuration} 
/>
</label>
