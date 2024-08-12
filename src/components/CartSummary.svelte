<script>
  export let items = [];
  export let total = 0;
  import src from '../assets/images/icon-order-confirmed.svg'
// export let onClose = () => {}; // Se usará para cerrar el modal desde el componente padre
</script>

<div class="cart-summary">
    <img {src} alt="" srcset="">
    <div class="cart-summary-model">
        <h1 class="cart-summary_title">Order Confirmed</h1>
        <span class="cart-summary_subtitle">We hope you enjoy your food!</span>
        <div class="cart-summary_content">
            {#each items as item}
                <div>
                    <div class="cart-summary_content-img-title">
                        <img src={item.image} alt="">
                        <div class="cart-summary_content-title">
                            <p>{item.subtitle}</p>
                            <div class="cart-summary_content-count-price">
                                <p>{item.count}x</p>
                                <span>@ ${item.price}</span>
                            </div>
                        </div>
                    </div>
                    <p class="cart-summary_content-total">${(item.count * item.price).toFixed(2)}</p>
                </div>
                <hr/>
            {/each}
            <div class="cart-summary_content-items-total">
                <span>Order Total</span>
                <h2>${total.toFixed(2)}</h2>
            </div>
        </div>
        <button>
            <p>Start New Order</p>
        </button>
    </div>    
  <!-- <button on:click={onClose}>Close</button> -->
</div>

<style lang="scss">
  .cart-summary {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    z-index: 101;
    height: fit-content;
    width: 40%;
    overflow-y: auto;
    max-height: calc(100vh - 210px);
    scroll-behavior: smooth;
    scrollbar-width: none;
    hr{
        height: 1px;
        background-color: var(--color-main-Rose-100);
        width: 100%;
        border: none;
    }
    *{
        margin: 0;
    }
    h1{
        color: var(--color-main-Rose-900);
        margin-top: 0;
        font-size: 40px;
    }
    .cart-summary-model{ 
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        div{
            border-radius: 8px;
        }
        button{
            background-color: var(--color-main-Red);
            color: var(--color-main-Rose-50);
            border: none;
            padding: 1rem;
            border-radius: 50px;
            font-size: var(--font-size-16);
            font-weight: var(--font-wight-400);
        }
    }
    .cart-summary_subtitle {
    font-size: var(--font-size-16);
    color: var(--color-main-Rose-400);
    font-weight: var(--font-wight-400);
    }   
    .cart-summary_content{
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-content: center;
        gap: 1rem;
        background-color: var(--color-main-Rose-50);
        padding: 1.5rem;
        border-radius: 8px;
        div:nth-child(n){
            display: flex;
            gap: 1rem;
        } 
        img{
            width: 12%;
            border-radius: 5px;
        }
        .cart-summary_content-title{
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            p{
                color: var(--color-main-Rose-900);
                font-weight: var(--font-wight-600);
            }
        }
        .cart-summary_content-count-price{
            display: flex;
            flex-direction: row;
            gap: 1rem;
            *{
                margin: 0;
            }
            span{
                font-size: var(--font-size-16);
                color: var(--color-main-Rose-400);
                font-weight: var(--font-wight-400);
            }
            p{
                color: var(--color-main-Red);
                font-weight: var(--font-wight-700);
            }
        }
        .cart-summary_content-total{
            font-size: var(--font-size-16);
            font-weight: var(--font-wight-600);
            color: var(--color-main-Rose-900);
            align-self: center;
        }
        .cart-summary_content-items-total{
            justify-content: space-between;
            align-items: center;
            span{
                color: var(--color-main-Rose-900);
                font-weight: var(--font-wight-400);
            }
            h2{
                color: var(--color-main-Rose-900);
                font-weight: var(--font-wight-700);
                font-size: 30px;
            }
        }
    }
  }
    @media only screen and (max-width: 375px){
        .cart-summary {
            width: 75%;
            h1{
                font-size: 24px;
            }
            img{
                display: none;
            }
        }
}

</style>
