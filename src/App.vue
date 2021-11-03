<template>
  <div class="container">
      <ProductList />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';

export default {
  name: 'App',
  components: {
    ProductList,
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
  color: $text-color;
  background: $bg-color;
}

.container {
  max-width: 1360px;
  margin: 0 auto;
  padding: 32px 5px 0;
  display: grid;
  grid-template-columns: 4fr 12fr;
  gap: 16px;
}
</style>
