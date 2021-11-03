<template>
  <div class="">
    <h1 class="title">Добавление товара</h1>
    <form class="form">
      <label for="name">
        <input class="form__input" type="text" name="name">
      </label>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
};
</script>

<style scoped lang="scss">
$bg-color: #fffefb;
$text-color: #3f3f3f;
$important-color: #ff8484;
$disabled-color: #eeeeee;
$bx-shodow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);

.title {
  font: {
    weight: 600;
    size: 28px;
  }
  line-height: 35px;
  margin-bottom: 16px;
}

%input {
  width: 100%;
}

.form {
  padding: 24px;
  border-radius: 4px;
  background: $bg-color;
  box-shadow: $bx-shodow;
  max-width: 320px;
  .form__input {
    @extend %input;
  }

}
</style>
