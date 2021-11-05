<template>
  <div>
    <div class="sorting">
    </div>
    <ul class="product-list">
      <li class="product" v-for="(product, index) in productList" :key="index">
        <img class="product__img" :src="product.url" alt="Картинка товара">
        <div class="product__text">
          <h1 class="product__title">{{ product.title }}</h1>
          <p class="product__description">{{ product.description }}</p>
          <p class="product__price">{{ product.price }} руб.</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
  props: ['productList'],
};
</script>

<style scoped lang="scss">
$bg-color: #fffefb;
$text-color: #3f3f3f;
$important-color: #ff8484;

.sorting {
  margin-left: auto;
  margin-bottom: 16px;
}

.product-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  .product {
    max-width: 320px;
    height: 423px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background-color: $bg-color;
    border-radius: 4px;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  }
  .product__img {
    max-width: 320px;
    max-height: 200px;
    margin: 0 auto;
  }
  .product__text {
    padding: 16px 16px 24px;
    min-height: 223px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    .product__title {
      font: {
        weight: 600;
        size: 20px;
      }
      line-height: 25px;
      margin-bottom: 11px;
    }
    .product__description {
      font-size: 16px;
      line-height: 20px;
      margin-bottom: auto;
    }
    .product__price {
      font: {
        weight: 600;
        size: 24px;
      }
      line-height: 30px;
    }
  }
}
</style>
