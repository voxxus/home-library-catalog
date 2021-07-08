<template>
  <div class="input">
    <p class="input__title">{{ inputTitle }}</p>
    <input
      :type="inputType"
      :placeholder="inputPlaceholder"
      :value="value"
      @input="$emit('input', $event.target.value)"
      class="input__field"
    />
  </div>
</template>

<script>
export default {
  name: "AppInput",
  props: {
    inputTitle: {
      type: String,
      default: "Поле ввода",
    },
    inputType: {
      type: String,
      default: "text",
    },
    inputPlaceholder: {
      type: String,
      default: "Поле ввода",
    },
    value: {
      type: String,
      default: "",
    },
  },
};
</script>

<style lang="scss" scoped>
.input {
  margin-bottom: 30px;

  &__title {
    margin-bottom: 10px;
    font-size: 18px;
  }

  &__field {
    height: 20px;
    padding: 5px;
  }
}
</style>
