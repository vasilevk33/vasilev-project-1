<script>
    let { drink, refill, stale, empty, chargeBank, chargeDevice, displayGoal, volumeUnit, toggleSimulation, isSimulating = $bindable(false), simulationAction = $bindable("Idle"),
    unitSystem = $bindable("Imperial"), waterGoal = $bindable(100), cleanDuration = $bindable(5), staleDuration = $bindable(10) 
    } = $props();
</script>

<h2>Controls</h2>
<button onclick={drink}>Drink ({unitSystem === "Imperial" ? "2 oz" : "60 ml"})</button>
<button onclick={refill}>Refill Water</button>
<button onclick={stale}>Make Water Stale</button>
<button onclick={empty}>Empty Water</button>
<button onclick={chargeDevice}>Charge External Device</button>
<button onclick={chargeBank}>Charge Power Bank (100%)</button>
<div class="simulation-panel">
  <h3>Simulation</h3>
  <button onclick={toggleSimulation}>
    {isSimulating ? "Pause Simulation" : "Start Simulation"}
  </button>
  <p>
    Important Status Update: {simulationAction}
  </p>
</div>

<style>
  button {
    display: block;
    width: 100%;
    height: 38px;
    box-sizing: border-box;
    padding: 10px 14px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 6px;
    background: #f0f0f0;
    color: #222;
    font-size: 14px;
    font-weight: 500;
    line-height: 16px;
    cursor: pointer;
    transition: background 0.2s;
  }

  button:hover {
    background: #e2e2e2;
  }

  .simulation-panel {
    margin-top: 24px;
    padding: 16px;
    background: #eef6ff;
    border: 1px solid #b9d7fb;
    border-radius: 8px;
  }

  .simulation-panel h3 {
    margin-top: 0;
    margin-bottom: 12px;
  }

  .simulation-panel button {
    background: #0284c7;
    color: white;
    border: none;
  }

  .simulation-panel button:hover {
    background: #0369a1;
  }

  .simulation-panel p {
    margin-bottom: 0;
    font-size: 13px;
    color: #333;
  }
</style>
