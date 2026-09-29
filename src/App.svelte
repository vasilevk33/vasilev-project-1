<script>
  import WaterBottleUI from './WaterBottleUI.svelte';
</script>

<div class="container">
  <div class="left-region">
    <section>
      <h2>Project Information</h2>
      <p>Project Title: Smart Water Bottle</p>
      <p>By: Kiki Vasilev</p>
      <p>Project Write Up: <a href="https://github.com/vasilevk33/vasilev-project-1/blob/main/README.md">Documentation</a></p>
      <button type="button">Info(Controls)</button>
    </section> 
  </div>
  <div class="right-region">
    <section class="display-section">
      <h2>Water Bottle Display</h2>
      <WaterBottleUI waterAmount={16} waterTemp={50} waterGoal={100} waterConsumedToday={38} userPreferedTemp={55} />
      <img class="bottle-sketch" src="WaterBottleSketch.png" alt="Water Bottle Sketch">
    </section>
  </div>
</div>

<style>
  .container {
    display: flex;
    height: 100vh;
    gap: 20px;
    padding: 20px;
    box-sizing: border-box;
    width: 100%;
  }
  .left-region {
    flex: 1;
    border-right: 1px solid #ccc;
    padding-right: 20px;
  }
  .right-region {
    flex: 2;
    display: flex;
    justify-content: center;
  }
  .display-section {
    display: flex;
    flex-direction: column;
    align-items: center; 
    text-align: center;
    width: 100%;
  }
  .display-section {
    display: flex;
    flex-direction: column;
    align-items: center; 
    text-align: center;
    width: 100%;
  }
</style>
