<script>
  import Cards from './components/Cards.svelte'
  import Cart from './components/Cart.svelte';
  import CartSummary from './components/CartSummary.svelte';

  let showSummary = false;
  let summaryItems = [];
  let summaryTotal = 0;

  const handleConfirm = (event) => {
    summaryItems = event.detail.items;
    summaryTotal = event.detail.total;
    showSummary = true;
  };
  function toggleSummary() {
    showSummary = !showSummary;
  }
</script>

<main>
  <!-- <button on:click={toggleSummary}>Confirm</button> -->
  <section class="main-cards">
    <h1>Desserts</h1>
    <Cards></Cards>
  </section>
  
  <section class="main-cart">
    <Cart on:confirm={handleConfirm} />
  </section>
  
  {#if showSummary}
    <div class="modal-background" on:click={() => showSummary = false}></div>
    <CartSummary items={summaryItems} total={summaryTotal} />
{/if}
</main>

<style>
  h1{
    color: var(--color-main-Rose-900);
    margin-top: 0;
    font-size: 40px;
  }
  main{
    margin: 5.2rem;
    display: grid;
    grid-template-columns: 1fr 0.5fr;
    grid-column-gap: 2rem;
  }
  .main-cards { grid-area: 1 / 1 / 3 / 2; }
  .main-cart { grid-area: 1 / 2 / 3 / 3; } 
  .modal-background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5); /* Fondo oscuro */
    backdrop-filter: blur(5px); /* Efecto de desenfoque */
    z-index: 100; /* Asegúrate de que esté por encima del contenido */
  }

  @media only screen and (max-width: 375px){
  main{
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: 1.2rem;
  }
}
</style>
