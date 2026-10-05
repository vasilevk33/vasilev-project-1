<script>
    let { drink, refill, stale, empty, chargeBank, chargeDevice, displayGoal, volumeUnit, toggleSimulation, isSimulating = $bindable(false), simulationAction = $bindable("Idle"),
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
<div class="simulation-panel">
  <h3>Simulation</h3>
  <button onclick={toggleSimulation}>
    {isSimulating ? "Pause Simulation" : "Start Simulation"}
  </button>
  <p>
    Important Status Update: {simulationAction}
  </p>
</div>
