<script>
    let ketchup = 0;
  
  const incrementKetchup = () => {
    ketchup += 1;
  }
  
  const decrementKetchup = () => {
    ketchup -= 1;
  }

    let mustard = 0;
    
    const incrementMustard = () => {
      mustard += 1;
    }
  
    
    const decrementMustard = () => {
      mustard -= 1;
    }
</script>

<main>
  <img src="./images/logo.png" alt="Hot Dog Quiz Logo"/>
  <div class="content">
    <section class="ketchup">
      <h2>KETChUP</h2>
      <div class="content-result font-freckle" aria-label="compteur ketchup 0">
        {ketchup}
      </div>
      <div class="content-controls">
        <button on:click={decrementKetchup} class="font-freckle" aria-label="boutton décrémentation ketchup">-</button>
        <button on:click={incrementKetchup} class="font-freckle" aria-label="boutton incrémentation ketchup">+</button>
      </div>
    </section>
    <section class="moutarde">
      <h2>Moutarde</h2>
      <div class="content-result font-freckle" aria-label="compteur moutarde 0">
        {mustard}
      </div>
      <div class="content-controls">
        <button on:click={decrementMustard} class="font-freckle" aria-label="boutton décrémentation moutarde">-</button>
        <button on:click={incrementMustard} class="font-freckle" aria-label="boutton incrémentation moutarde">+</button>
      </div>
    </section>
  </div>
</main>

<style>
</style>
