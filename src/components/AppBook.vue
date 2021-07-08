<template>
  <div class="book">
    <div class="book__spine spine">
      <div class="spine__author">
        {{ book.author }}
      </div>
      <div class="spine__title">
        {{ book.title }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppBook",
  props: {
    book: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style scoped>
.spine {
  display: flex;
  justify-content: space-around;
  align-items: center;
  min-height: 50px;
  width: 100%;
  border: 2px solid black;
  border-radius: 6px;
  background-color: gray;
}
</style>
