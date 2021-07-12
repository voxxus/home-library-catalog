<template>
  <div class="modal">
    <div class="modal__outer">
      <div class="modal__window">
        <div class="modal__header">
          <h3 class="modal__title">
            <slot name="title">Заголовок</slot>
          </h3>
        </div>
        <div class="modal__content">
          <slot name="content">Контент</slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppModalWindow",
};
</script>

<style lang="scss" scoped>
.modal {
  &__outer {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 150;
    background-color: rgba(0, 0, 0, 0.5);
  }

  &__window {
    width: 20vw;
    background-color: #fff;
    border: 1px solid #000;
    border-radius: 6px;
  }

  &__title {
    border-bottom: 1px solid #000;
  }

  &__title,
  &__content {
    padding: 10px;
  }
}
</style>
