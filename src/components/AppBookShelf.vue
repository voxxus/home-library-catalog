<template>
  <div class="bookshelf">
    <div class="bookshelf__controls">
      <div class="bookshelf__sort-author">
        <span class="bookshelf__sort-text">По автору</span>
        <span class="bookshelf__arrow-up"></span>
        <span class="bookshelf__arrow-down"></span>
      </div>
      <div class="bookshelf__sort-title">
        <span class="bookshelf__sort-text">По названию</span>
        <span class="bookshelf__arrow-up"></span>
        <span class="bookshelf__arrow-down"></span>
      </div>
      <button class="button bookshelf__btn-reset">Сброс</button>
      <button @click="$emit('addBook')" class="button bookshelf__btn-add">
        Добавить книгу
      </button>
    </div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "AppBookShelf",
};
</script>

<style lang="scss" scoped>
.bookshelf {
  max-width: 30%;
  min-height: 30%;
  border: 3px solid black;
  background-color: rgba(165, 42, 42, 0.83);
  padding: 10px 10px 0;

  &__controls {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
  }
}
</style>
