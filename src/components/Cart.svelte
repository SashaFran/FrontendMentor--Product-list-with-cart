<script>
    import { cart } from '../store.js';
    import src from '../assets/images/illustration-empty-cart.svg';
    import srcRem from '../assets/images/icon-remove-item.svg';
    import srcCarbon from '../assets/images/icon-carbon-neutral.svg';
    let cartItems = [];
  
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    cart.subscribe(items => {
        cartItems = items;
    });

    const confirmOrder = () => {
        dispatch('confirm', { items: cartItems, total });
    };

    cart.subscribe(items => {
    cartItems = items;
  });

  const deleteItem = (title) => {
    cart.update(items => {
      const index = items.findIndex(item => item.title === title);
      if (index !== -1) {
        items.splice(index, 1);
      }
      return items;
    });
  };

$: total = cartItems.reduce((sum, item) => sum + item.price * item.count, 0);
</script>

<article>
    <h2>Your Cart ({cartItems.length})</h2>
    {#if cartItems.length > 0}
    <div class="cart">
        {#each cartItems as item}
        <div class="cart-content">
            <div class="cart-content_item">
                <p class="cart-content_title">{item.subtitle}</p>
                <div class="cart-content_item-count-price">
                    <div class="cart-content_count">
                        <p>{item.count}x</p>
                    </div>
                    <div class="cart-content_price">
                        <p><span>@</span>${item.price}</p>
                        <p class="cart-content_total-price">
                            ${item.count > 1 ? (parseFloat(item.count) * parseFloat(item.price)).toFixed(2) : item.price}
                        </p>                    
                    </div>
                </div>
            </div>
            <div style="align-content: center;">
                <button on:click={() => deleteItem(item.title)}> 
                    <img src={srcRem} alt="Delete icon" srcset="">
                </button>
            </div>
        </div>
        <hr/>
        {/each}
    </div>
    <div>
    <div class="cart-total">
        <p class="cart-content_total-price">Total</p>  
        <h2>${total.toFixed(2)}</h2> 
      </div>
    </div>
    <div class="carbol-neutral">  
        <img src={srcCarbon} alt="">
        <p>This is a <span>carbon-neutral</span> delivery</p>
    </div>
    <button class="confirm" on:click={confirmOrder}>Confirm Order</button>
    {:else if cartItems.length == 0}
        <div class="cart-empty">
            <img src={src} alt="empty-cart" srcset="">
            <span>Your added items will appear here</span>
        </div>
    {/if}
</article>

<style lang="scss">
    hr{
        height: 1px;
        background-color: var(--color-main-Rose-300);
        width: 100%;
        border: none;
    }
    article{
        height: fit-content;
        padding: 1.5rem;
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        background-color: white;
        border-radius: 8px;
        gap: 1rem;
        font-family: var(--font-family);
        h2{
            color: var(--color-main-Red);
            font-weight: var(--font-wight-700);
            margin: 0;
        }
        .cart-empty{
            display: flex;
            flex-direction: column;
            width: fit-content;
            align-items: center;
            align-self: center;
            padding: 2rem;
            gap: 1rem;
            span{
                font-weight: var(--font-wight-600);
                color: var(--color-main-Rose-500);
                font-size: var(--font-size-16);
            }
        }
        .cart{
           display: flex;
            justify-content: space-around;
            flex-direction: column;
            gap: 0.5rem; 
        }
        .cart-content, .cart-total, .carbol-neutral{
            display: flex;
            justify-content: space-between;
            flex-direction: row;
            gap: 0.5rem; 
            align-items: center;
            *{
                margin: 0;
            }

        }
        .carbol-neutral{
            display: flex;
            flex-direction: row;
            gap: 0.5rem; 
            align-items: center;
            justify-content: center;
            padding: 1rem;
            background-color: var(--color-main-Rose-100);
            color: var(--color-main-Rose-900);
            border-radius: 5px;
            font-size: var(--font-size-14);
            span{
                font-weight: var(--font-wight-600);
            }
        }
        .cart-total{
            p{
                font-weight: var(--font-wight-600);
                color: var(--color-main-Rose-400);
            }
            h2{
                font-weight: var(--font-wight-700);
                color: var(--color-main-Rose-900);
                font-size: 30px;
            }
        }
        .cart-content{
            p{
                margin: 0;
            }
            .cart-content_item{
                flex-direction: column;
            }
            .cart-content_item, .cart-content_item-count-price{
                display: flex;
                justify-content: space-between;
                gap: 1rem;
            }
            .cart-content_item-count-price{
                display: flex;
            }
            .cart-content_count{
                display: flex;
                gap: 0.2rem;
                *{
                    margin: 0;
                }
                p{
                color: var(--color-main-Red);
                font-weight: var(--font-wight-700);
                }
            }
        }
        .cart-content_title{
            color: var(--color-main-Rose-900);
            font-weight: var(--font-wight-600);
        } 
        .cart-content button{
            background-color: transparent;
            border: 1px solid var(--color-main-Rose-300);
            border-radius: 50%;
            cursor: pointer;
        }
        .cart-content_price{
                display: flex;
                gap: 0.5rem;
                font-weight: var(--font-wight-400);
                color: var(--color-main-Rose-400);
                *{
                    margin: 0;
                }
                span{
                    color: var(--color-main-Rose-300);
                    font-weight: var(--font-wight-400);
                    font-size: var(--font-size-14);
                    padding: 0 0.2rem 0 0;
                }
                .cart-content_total-price{
                    font-weight: var(--font-wight-600);
                }
        }
        .confirm{
            background-color: var(--color-main-Red);
            color: var(--color-main-Rose-50);
            border: none;
            border-radius: 50px;
            padding: 1rem;
            font-size: var(--font-size-16);
            font-weight: var(--font-wight-500);
            font-family: var(--font-family);
            cursor: pointer;
        }
    }

</style>