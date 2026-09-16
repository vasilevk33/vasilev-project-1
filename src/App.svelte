<script>
  import WaterBottleUI from './WaterBottleUI.svelte';
</script>

<section>
  <h2>Project Information</h2>
  <p>Project: Smart Water Bottle</p>
  <p>Name: Kiki Vasilev</p>
</section>

<section>
  <h2>Water Bottle Display</h2>
  <WaterBottleUI waterAmount={16} waterTemp={50} waterGoal={100} waterConsumedToday={38} userPreferedTemp={55} />
</section>

<style>
  section {
    margin-bottom: 250px;
  }
</style>
