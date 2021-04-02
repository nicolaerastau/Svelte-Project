<script>
  import Product from "./Product.svelte";
  import Button from "./Button.svelte";
  import Cart from "./Cart.svelte";

  let title = "";
  let price = "";
  let description = "";

  let products = [];
  let cartItems = [];
  let bgImage='../images/background.jpg';

  function setTitle(event) {
    title = event.target.value;
  }

  function createProduct() {
    const newProduct = {
      title: title,
      price: price,
      description: description
    };

    products = [...products, newProduct];
    //products = products.concat(newProduct);
  }

  function removeProduct(e) {
    //const title = e.detail;
    products = products.filter(prod => prod.title !== e.detail);
  }

  function addToCart(event) {
    const selectedTitle = event.detail;
    cartItems = cartItems.concat({
      ...products.find(prod => prod.title === selectedTitle)
    });
  }
</script>

<style>
/* .background { 
   background-image: url('public/images/background.jpg');
} */
  .background {
    height:auto;
    display:flex;
    align-items:center;
    background-size: cover;
    background:no-repeat center center fixed;
  }
  .container {
    width: 100%;
    background-color: rgb(67, 125, 151);
    padding: 10px;
    display: block;
    margin: 30px auto;
    border-radius: 10px;
   
  }
  @media (min-width: 768px) {
    .container {
      width: 25rem;
    }
  }

  .section {
    width: 22rem;
    height: auto;
    margin: auto;
  }
  @media (max-width: 767px) {
    .section {
      width: 17rem;
      padding: 10px;
      margin: auto;
    }
  }

  label {
    background-color: rgb(6, 166, 194);
    margin-bottom: 0.5rem;
    margin-left: 0;
    width: 40%;
    height: 1.5rem;
    color: #fff;
    text-align: center;
    border-radius: 3px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  input,
  textarea {
    width: 100%;
    border-radius: 4px;
    color: #333;
  }
  p {
    color: #fff;
  }
  .title {
    margin-top: 10px;
    margin-bottom: 10px;
  }
  @media (max-width: 465px) {
    .title,
    .price,
    .description {
      width: 14rem;
    }
  }
</style>


<section>
  <Cart items={cartItems} />
  <!-- <img src="./public/images/bacground.jpg" alt=""/> -->
</section>

<hr />

<div class="background" style="background-image:url('{bgImage}')">
<div class="container">
  <section class="section">

    <div class="title">
      <label for="title">Title</label>
      <input type="text" id="title" value={title} on:input={setTitle} />
    </div>
    <div class="price">
      <label for="price">Price</label>
      <input type="number" id="price" bind:value={price} />
    </div>
    <div class="description">
      <label for="description">Description</label>
      <textarea rows="3" bind:value={description} />
    </div>

    <Button buttonPrimary on:click={createProduct}>Create Product</Button>
  </section>

  <section>
    {#if products.length === 0}
      <p>No products were added yet!</p>
    {:else}
      {#each products as product}
        <Product
          productTitle={product.title}
          productPrice={product.price}
          productDescription={product.description}
          on:addcart={addToCart}
          on:removeproduct={removeProduct} />
      {/each}
    {/if}
  </section>
</div>
</div>