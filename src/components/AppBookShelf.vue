<template>
  <div class="bookshelf">
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.bookshelf {
  max-width: 30%;
  min-height: 30%;
  border: 3px solid black;
  background-color: rgba(165, 42, 42, 0.83);
  padding: 10px 10px 0;
}
</style>
