<template>
  <div class="form__inner">
    <h1 class="title">Добавление товара</h1>
    <form class="form">
      <label class="form__label" for="name">
        <p class="label__title label__title--important">Наименование товара</p>
        <input required class="form__input" type="text" name="name" placeholder="Введите наименование товара" v-model="title" @blur="notEmpty" title="Поле является обязательным">
        <p class="input-error" hidden>{{ invalidMessage }}</p>
      </label>
      <label class="form__label" for="description">
        <p class="label__title">Описание товара</p>
        <textarea class="form__input--area" name="description" placeholder="Введите описание товара" v-model="description"></textarea>
      </label>
      <label class="form__label" for="image">
        <p class="label__title label__title--important">Ссылка на изображение товара</p>
        <input required class="form__input" type="url" name="image" placeholder="Введите ссылку " v-model="url" @blur="notEmpty" title="Поле является обязательным">
        <p class="input-error" hidden>{{ invalidMessage }}</p>
      </label>
      <label class="form__label" for="price">
        <p class="label__title label__title--important">Цена товара</p>
        <input required class="form__input" type="number" name="price" placeholder="Введите цену" v-model="price" @blur="notEmpty" title="Поле является обязательным">
        <p class="input-error" hidden>{{ invalidMessage }}</p>
      </label>
      <button :disabled="!areAllInputsValid" class="button" type="button" @click="createNewProduct">Добавить товар</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data() {
    return {
      title: '',
      url: '',
      description: '',
      price: '',
      invalidMessage: 'Поле является обязательным',
    };
  },
  computed: {
    isTitleValid() {
      return this.title !== '';
    },
    isUrlValid() {
      const regex = RegExp('(https?:\\/\\/)?((([a-z\\d]([a-z\\d-]*[a-z\\d])*)\\.)+[a-z]{2,}|((\\d{1,3}\\.){3}\\d{1,3}))(\\:\\d+)?(\\/[-a-z\\d%_.~+@]*)*(\\?[;&a-z\\d%_.~+=-@]*)?(\\#[-a-z\\d_@]*)?$', 'i');
      return this.url !== '' && this.url.match(regex);
    },
    isPriceValid() {
      return this.price !== '';
    },
    areAllInputsValid() {
      return this.isTitleValid && this.isUrlValid && this.isPriceValid;
    },
  },
  methods: {
    createNewProduct() {
      const newProduct = {
        title: this.title,
        url: this.url,
        description: this.description,
        price: this.price,
      };
      this.$emit('addProduct', newProduct);
    },
    notEmpty(event) {
      if (event.target.value === '') {
        event.target.classList.add('invalid');
      } else {
        event.target.classList.remove('invalid');
      }
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

.form__inner {
  margin: 0 auto;
}

.title {
  font: {
    weight: 600;
    size: 28px;
  }
  line-height: 35px;
  margin-bottom: 16px;
}

%style-input {
  display: block;
  width: 100%;
  height: 36px;
  padding: 10px 5px 11px 16px;
  border-radius: 4px;
  border: none;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  color: $text-color;
  cursor: pointer;
}

%style-placeholder {
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
    .input-error {
      position: absolute;
      font-size: 8px;
      line-height: 10px;
      letter-spacing: -0.02em;
      color: $important-color;
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
    @extend %style-input;
    &::placeholder {
      @extend %style-placeholder;
    }
    &:focus {
      outline: none;
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
    @extend %style-input;
    height: 108px;
    resize: none;
    overflow: hidden;
    white-space: pre-wrap;
    &::placeholder {
      @extend %style-placeholder;
    }
    &:focus {
      outline: none;
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

.invalid {
  border: 1px solid $important-color !important;
}
</style>
