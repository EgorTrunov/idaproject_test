<template>
  <div class="">
    <h1 class="title">Добавление товара</h1>
    <form class="form">
      <label class="form__label" for="name">
        <p class="label__title label__title--important">Наименование товара</p>
        <input required class="form__input" type="text" name="name" placeholder="Введите наименование товара" v-on:input="newName">
      </label>
      <label class="form__label" for="description">
        <p class="label__title">Описание товара</p>
        <textarea class="form__input--area" name="description" placeholder="Введите описание товара" v-on:input="newDescription"></textarea>
      </label>
      <label class="form__label" for="image">
        <p class="label__title label__title--important">Ссылка на изображение товара</p>
        <input required class="form__input" type="text" name="image" placeholder="Введите ссылку " v-on:input="newImg">
      </label>
      <label class="form__label" for="price">
        <p class="label__title label__title--important">Цена товара</p>
        <input required class="form__input" type="text" name="price" placeholder="Введите цену" v-on:input="newPrice">
      </label>
      <button class="button" type="button" @click="createNewProduct">Добавить товар</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data() {
    return {
      product: {
        title: '',
        url: '',
        description: '',
        price: '',
      },
    };
  },
  methods: {
    newName(event) {
      this.product.title = event.target.value;
    },
    newDescription(event) {
      this.product.description = event.target.value;
    },
    newImg(event) {
      this.product.url = event.target.value;
    },
    newPrice(event) {
      this.product.price = event.target.value;
    },
    createNewProduct() {
      this.$emit('addProduct', this.product);
    },
  },
};
</script>

<style scoped lang="scss">
$bg-color: #fffefb;
$text-color: #3f3f3f;
$label-color: #49485e;
$placeholder-color: #b4b4b4;
$important-color: #ff8484;
$disabled-color: #eeeeee;
$active-color: #7bae73;
$active-color--text: #ffffff;

.title {
  font: {
    weight: 600;
    size: 28px;
  }
  line-height: 35px;
  margin-bottom: 16px;
}

%input {
  display: block;
  width: 100%;
  height: 36px;
  padding: 10px 5px 11px 16px;
  border: none;
  border-radius: 4px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  color: $text-color;
  cursor: pointer;
}

%placeholder {
  color: $placeholder-color;
}

.form {
  padding: 24px;
  border-radius: 4px;
  background: $bg-color;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  max-width: 320px;
  .form__label {
    display: block;
    margin-bottom: 16px;
    .label__title {
      font-size: 10px;
      line-height: 12px;
      color: $label-color;
      position: relative;
      margin-bottom: 4px;
    }
  }
  .label__title--important::after {
    content: '';
    position: absolute;
    height: 4px;
    width: 4px;
    background-color: $important-color;
    border-radius: 4px;
  }
  .form__input {
    @extend %input;
    &::placeholder {
      @extend %placeholder;
    }
    &:focus {
      outline: none;
    }
    &:invalid:not(:focus) {
      border: 1px solid $important-color;
    }
  }
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
  input[type=number] {
    -moz-appearance: textfield;
  }
  .form__input--area {
    @extend %input;
    height: 108px;
    resize: none;
    overflow: hidden;
    white-space: pre-wrap;
    &::placeholder {
      @extend %placeholder;
    }
  }
  .button {
    width: 100%;
    height: 36px;
    font: {
      family: 'Inter', sans-serif;
      weight: 600;
    }
    text-align: center;
    border: none;
    border-radius: 10px;
    margin-top: 8px;
    padding: 10px auto;
    background-color: $active-color;
    color: $active-color--text;
    &:disabled {
      color: $placeholder-color;
      background: $disabled-color;
    }
  }
}
</style>
