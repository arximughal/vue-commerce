<template>
  <div class="categories-container">
    <h3>Shop Categories</h3>
    <p v-if="isFetching">Loading...</p>
    <ul>
      <li v-for="category in categories" :key="category">{{ category }}</li>
    </ul>
  </div>
  <div class="products">
    <h3>Products</h3>
    <p v-if="isFetching">Loading...</p>
    <div class="products-list">
      <div class="product" v-for="product in products" :key="product.id">
        <img :src="product.image" />
        <div class="product-info">
          <h4>{{product.title}}</h4>
          <h2>${{product.price}}</h2>
          <button class="buy-now-btn" type="button" name="button">
            Buy Now
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style media="screen">
  .categories-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .categories-container ul {
    list-style: none;
    float: right;
    display: inline-flex;
    padding: 0;
    margin: 0;
  }
  .categories-container ul li {
    display: inline;
    padding: 10px 20px;
    border: 1px solid #333;
    border-radius: 8px;
    margin-right: 5px;
    cursor: pointer;
    text-transform: uppercase;
  }
  .products-list {
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
    -webkit-flex-direction: row;
    -ms-flex-direction: row;
    flex-direction: row;
    -webkit-flex-wrap: wrap;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    -webkit-justify-content: flex-start;
    -ms-flex-pack: start;
    justify-content: flex-start;
    -webkit-align-content: stretch;
    -ms-flex-line-pack: stretch;
    align-content: stretch;
    -webkit-align-items: flex-start;
    -ms-flex-align: start;
    align-items: flex-start;
  }
  .product {
    display: flex;
    flex-direction: column;
    width: 30%;
    padding: 10px;
    transition: all 0.2s ease-in-out;
    cursor: pointer;
  }
  .product:hover {
    background: #e6e6e6;
  }
  .product img {
    width: 100%;
    height: 200px;
    object-fit: contain;
    object-position: center;
  }
  .product-info {
    display: flex;
    width: 100% !important;
    flex-direction: column;
  }
  .product-info h2 {
    padding: 0;
    margin: 0;
  }
  .buy-now-btn {
    box-shadow: 0px 1px 0px 0px #fff6af;
    background:linear-gradient(to bottom, #ffec64 5%, #ffab23 100%);
    background-color:#ffec64;
    border-radius:6px;
    border:1px solid #ffaa22;
    display:inline-block;
    cursor:pointer;
    color:#333333;
    font-family:Arial;
    font-size:15px;
    font-weight:bold;
    padding:6px 24px;
    text-decoration:none;
    text-shadow:0px 1px 0px #ffee66;
  }
  .buy-now-btn:hover {
    background:linear-gradient(to bottom, #ffab23 5%, #ffec64 100%);
    background-color:#ffab23;
  }
  .buy-now-btn:active {
    position:relative;
    top:1px;
  }

</style>


<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  data: () => {
    return {
      products: [],
      categories: [],
      isFetching: false
    }
  },
  methods: {
    async getCategories () {
      this.isFetching = true;
      const response = await fetch('https://fakestoreapi.com/products/categories').then(res => { return res.json(); }).catch(e => { console.log(e) });
      this.categories = response;
      this.isFetching = false;
    },
    async getProducts () {
      this.isFetching = true;
      const response = await fetch('https://fakestoreapi.com/products').then(res => { return res.json(); }).catch(e => { console.log(e) });
      this.products = response;
      this.isFetching = false;
    }
  },
  mounted() {
    this.getCategories();
    this.getProducts();
  },
}
</script>
