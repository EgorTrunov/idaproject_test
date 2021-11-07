<template>
  <div class="container">
      <Form @add-product="addProduct"/>
      <ProductList :product-list="productList" @delete-product="deleteProduct"/>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import Form from './components/Form.vue';

export default {
  name: 'App',
  components: {
    ProductList, Form,
  },
  data() {
    return {
      productList: [
        {
          title: 'Наименование товара',
          url: 'https://audeze.su/wp-content/uploads/2018/05/Audeze-Mobius-Product-Shots-Oct-2018-Carbon3Q_Mic_2000x-600x600.jpg',
          description: 'Описание товара. Что-то интересное о товаре',
          price: '2000',
        },
        {
          title: 'Наименование товара',
          url: 'https://audeze.su/wp-content/uploads/2018/05/Audeze-Mobius-Product-Shots-Oct-2018-Carbon3Q_Mic_2000x-600x600.jpg',
          description: 'Описание товара. Что-то интересное о товаре #2',
          price: '5000',
        },
      ],
    };
  },
  methods: {
    addProduct(newProduct) {
      this.productList.unshift(newProduct);
      localStorage.setItem('productList', JSON.stringify(this.productList));
    },
    deleteProduct(index) {
      this.productList.splice(index, 1);
      localStorage.setItem('productList', JSON.stringify(this.productList));
    },
  },
  mounted() {
    const storedProductList = JSON.parse(localStorage.getItem('productList'));
    if (storedProductList) {
      this.productList = storedProductList;
    }
  },
};
</script>

<style lang="scss">
  $bg-color: #fffefb80;
  $text-color: #3f3f3f;

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font: {
    family: 'Source Sans Pro', sans-serif;
    size: 12px;
    weight: 400;
  }
  line-height: 15px;
  color: $text-color;
}

.container {
  max-width: 1360px;
  padding: 32px 5px 0;
  display: grid;
  grid-template-columns: 1fr 3fr;
  gap: 16px;
  margin: 0 auto;
}

@media (max-width: 1100px) {
  .container {
    grid-template-columns: 1fr 2fr;
  }
}

@media (max-width: 850px) {
  .container {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 550px) {
  .container {
    grid-template-columns: 1fr;
  }
}
</style>
