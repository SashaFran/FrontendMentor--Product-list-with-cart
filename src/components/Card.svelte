<script>
  import { cart } from '../store.js';
  import srcCart from '../assets/images/icon-add-to-cart.svg';
  import srcSum from '../assets/images/icon-increment-quantity.svg';
  import srcRes from '../assets/images/icon-decrement-quantity.svg';
  export let image;
  export let title;
  export let subtitle;
  export let price;

  let count = 0

  const increment = () => {
    count += 1
    updateCart();
  }

   const decrement = () => {
    count -= 1
     updateCart();
  }

  const updateCart = () => {
    cart.update(items => {
      const itemIndex = items.findIndex(item => item.title === title);
      if (itemIndex > -1) {
        if (count > 0) {
          items[itemIndex].count = count;
        } else {
          items.splice(itemIndex, 1);
        }
      } else {
        items = [...items, { title, image, subtitle, price, count }];
      }
      return items;
    });
  };

</script>

<div class="card">
  {#if count > 0}
    <img src={image} alt={title} class="card-image-added" />
	  <div class="card-cart_added">
      <button class="card-cart_inc" on:click={increment}>
        <img src={srcSum} alt="icon-increment-quantity" srcset="">
      </button>
      <p>{count}</p> 
      <button class="card-cart_dec" on:click={decrement}>
        <img src={srcRes} alt="icon-decrement-quantity" srcset="">
      </button>
    </div>
  {:else}
    <img src={image} alt={title} class="card-image" />
    <button class="card-cart" on:click={increment}>
      <img src={srcCart} alt="add-to-cart" srcset="">
      <p>Add to Cart</p>
    </button>
  {/if}

  <div class="card-content">
    <span class="card-subtitle">{title}</span>
    <h3 class="card-title">{subtitle}</h3>
    <p class="card-price">${price}</p>
  </div>
</div>

<style lang="scss">

  .card {    
    max-width: 100%;
    display: flex;
    flex-direction: column;
    gap: 2rem;
    position: relative;
  }
  .card-cart{
    background-color: white;
    outline: 1px solid var(--color-main-Rose-400);
    border: none;
    cursor: pointer;
    justify-content: center;
    * {
      margin: 0.6rem 0 0.6rem 0;
      font-size: var(--font-size-14);
      font-weight: var(--font-wight-600);
      font-family: var(--font-family);
      color: var(--color-main-Rose-900);
    }
  }
  .card-cart, .card-cart_added{
    display: flex;
    align-items: center;
    gap: 0.5rem;
    width: 60%;
    border-radius: 40px;
    position: absolute;
    bottom: calc(15rem - 45%);
    left: 50%;
    transform: translateX(-50%);
    padding: 0;
  }
  .card-cart_added{
    justify-content:space-around;
    background-color: var(--color-main-Red);
    color: white;
    border: none;
    * {
      font-size: var(--font-size-14);
      font-weight: var(--font-wight-600);
      margin: 0.6rem 0 0.6rem 0;
    }
  }
  .card-cart_inc, .card-cart_dec{
    border: solid 1px white;
    border-radius: 50%;
    background-color: transparent;
    display: flex;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 20px;
    height: 20px;
  }
  .card-image, .card-image-added{
    width: 100%;
    height: auto;
    border-radius: 8px;
  }
  .card-image-added{
    outline: 3px solid var(--color-main-Red);
  }

  .card-content{
    *{
      margin: 0.2rem 0 0.2rem 0;
    }
  }

  .card-title {
    font-size: var(--font-size-16);
    color: var(--color-main-Rose-900);
    font-weight: var(--font-wight-600);
  }

  .card-subtitle {
    font-size: var(--font-size-14);
    color: var(--color-main-Rose-400);
    font-weight: var(--font-wight-400);
  }

  .card-price {
    font-size: var(--font-size-16);
    color: var(--color-main-Red);
    font-weight: var(--font-wight-600);
  }
</style>
