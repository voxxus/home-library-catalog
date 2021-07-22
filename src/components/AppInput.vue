<template>
  <div class="input">
    <div class="input__title">
      <p class="input__title-text">{{ inputTitle }}</p>
      <span v-if="required" class="input__required"> *</span>
    </div>
    <input
      :type="inputType"
      :placeholder="inputPlaceholder"
      :value="value"
      :required="required"
      class="input__field"
      @input="$emit('input', $event.target.value)"
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

    required: {
      type: Boolean,
      default: false,
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

  &__title-text {
    display: inline-block;
  }

  &__required {
    color: red;
  }

  &__field {
    padding: 5px;

    &::placeholder {
      font-size: 11px;
    }
  }
}
</style>
