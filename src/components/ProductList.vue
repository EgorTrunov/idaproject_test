<template>
  <div class="product__inner">
    <div class="sorting">
      <div class="select" @click="areOptionVisible = !areOptionVisible" key="transferFrom">
        <p class="select--active">{{ optionActive }}</p>
        <div class="option__inner" v-if="areOptionVisible">
            <span class="option__item" v-for="option in options" :key="option.value" @click="selectOption(option.name)">{{ option.name }}</span>
        </div>
        <span class="select__arrow">
          <img class="img__arrow" src="@/assets/img/arrow.svg" v-if="!areOptionVisible">
          <img class="img__arrow" src="@/assets/img/arrow-rotate.svg" v-else>
        </span>
      </div>
    </div>
    <transition-group tag="ul" class="product-list" name="list">
      <li class="product" v-for="(product, index) in productList" :key="index">
        <div class="box-svg" @click="deleteProduct(index)">
          <img src="@/assets/img/delete.svg">
        </div>
        <img class="product__img" :src="product.url" alt="Картинка товара">
        <div class="product__text">
          <h1 class="product__title">{{ product.title }}</h1>
          <p class="product__description">{{ product.description }}</p>
          <p class="product__price">{{ product.price }} руб.</p>
        </div>
      </li>
      </transition-group>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
  props: ['productList'],
  data() {
    return {
      options: [
        { name: 'По цене min', value: 'min' },
        { name: 'По цене max', value: 'max' },
        { name: 'По наименованию', value: 'title' },
      ],
      optionActive: 'По умолчанию',
      areOptionVisible: false,
      sortedProducts: [],
    };
  },
  methods: {
    deleteProduct(index) {
      this.$emit('deleteProduct', index);
    },
    selectOption(name) {
      this.optionActive = name;
    },
  },
};
</script>

<style scoped lang="scss">
$bg-color: #fffefb;
$text-color: #3f3f3f;
$important-color: #ff8484;
$select-color: #b4b4b4;

.product__inner {
  margin: 0 auto;
}

.sorting {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 16px;
  position: relative;
  .select {
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 121px;
    padding: 10px 16px 11px;
    position: relative;
    cursor: pointer;
    color: $select-color;
    background: $bg-color;
    border-radius: 4px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  }
  .select--active {
    margin-right: 5px;
    color: $select-color;
  }
  .option__inner {
    min-width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    position: absolute;
    background: $bg-color;
    border-radius: 4px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    top: 32px;
    right: 0;
    span {
      width: 100%;
      padding: 8px;
      color: $select-color;
      &:hover {
        background: $select-color;
        opacity: 0.5;
        color: $text-color;
        border-radius: 4px;
      }
    }
  }
  .img__arrow {
    display: block;
  }
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
    position: relative;
    .box-svg {
      display: none;
      position: absolute;
      right: -8px;
      top: -8px;
      width: 32px;
      padding: 8px;
      background: #FF8484;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
      border-radius: 10px;
      img {
        display: block;
      }
    }
    &:hover {
      .box-svg {
        display: block;
        cursor: pointer;
      }
    }
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

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

@media (max-width: 1100px) {
  .product-list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 850px) {
  .product-list {
    grid-template-columns: repeat(1, 1fr);
  }
}

@media (max-width: 550px) {
  .sorting {
    justify-content: flex-start;
  }
}
</style>
