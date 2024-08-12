<script>
  import Card from './Card.svelte';
  
  import image1 from '../assets/images/image-waffle-desktop.jpg';
  import image2 from '../assets/images/image-creme-brulee-desktop.jpg';
  import image3 from '../assets/images/image-macaron-desktop.jpg';
  import image4 from '../assets/images/image-tiramisu-desktop.jpg';
  import image5 from '../assets/images/image-baklava-desktop.jpg';
  import image6 from '../assets/images/image-meringue-desktop.jpg';
  import image7 from '../assets/images/image-cake-desktop.jpg';
  import image8 from '../assets/images/image-brownie-desktop.jpg';
  import image9 from '../assets/images/image-panna-cotta-desktop.jpg';

  const items = [
    {
      image: image1,
      title: 'Waffle',
      subtitle: 'Waffle with Berries',
      price: '6.50'
    },
    {
      image: image2,
      title: 'Créme Brulée',
      subtitle: 'Vanilla Bean Créme Brulée',
      price: '7.00'
    },
    {
      image: image3,
      title: 'Macaron',
      subtitle: 'Macaron Mix of Five',
      price: '8.00'
    },
    {
      image: image4,
      title: 'Tiramisu',
      subtitle: 'Classic Tiramisu',
      price: '5.50'
    },
    {
      image: image5,
      title: 'Baklava',
      subtitle: 'Pistachio Baklava',
      price: '4.00'
    },
    {
      image: image6,
      title: 'Pie',
      subtitle: 'Lemon Meringue Pie',
      price: '5.00'
    },
    {
      image: image7,
      title: 'Cake',
      subtitle: 'Red Velvet Cake',
      price: '4.50'
    },
    {
      image: image8,
      title: 'Brownie',
      subtitle: 'Salted Caramel Brownie',
      price: '5.50'
    },
        {
      image: image9,
      title: 'Panna Cotta',
      subtitle: 'Vanilla Panna Cotta',
      price: '6.50'
    }
  ];
</script>

<div class="grid">
  {#each items as item}
    <Card 
      image={item.image} 
      title={item.title} 
      subtitle={item.subtitle} 
      price={item.price} 
    />
  {/each}
</div>

<style>
   .grid {
    display: grid;
    grid-template-columns:  repeat(3, minmax(200px, 1fr)); /* 3 columnas que se ajustan al contenido */
    grid-column-gap: 1.5em;
    grid-row-gap: 1.5em;
    justify-content: center; 
  }
  @media only screen and (max-width: 375px){
  .grid {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: 1.2rem;
  }
}
</style>