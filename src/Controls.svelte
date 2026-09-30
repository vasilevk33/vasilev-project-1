<script>
    let { drink, refill, stale, chargeBank, chargeDevice } = $props();
</script>

<h2>Test Controls</h2>
<button onclick={drink}>Drink (2 oz)</button>
<button onclick={refill}>Refill Water</button>
<button onclick={stale}>Make Water Stale</button>
<button onclick={chargeBank}>Charge Power Bank (100%)</button>
<button onclick={chargeDevice}>Charge External Device</button>
