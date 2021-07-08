<template>
  <ul class="list">
    <li v-for="(item, index) in items" :key="index" class="list__item">
      <slot name="items" :item="item" />
    </li>
  </ul>
</template>

<script>
export default {
  name: "AppList",
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.list {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
</style>
