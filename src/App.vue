<template>
  <div id="app">
    <app-list :items="shelves">
      <template #items="{ item: books }">
        <app-list :items="books">
          <template #items="{ item: book }">
            {{ book }}
          </template>
        </app-list>
      </template>
    </app-list>
  </div>
</template>

<script>
import booksData from "./mock/books.json";
import AppList from "@/components/AppList";

export default {
  name: "App",
  components: {
    AppList,
  },
  data() {
    return {
      shelves: null,
    };
  },
  created() {
    const firstShelf = booksData.slice(0, 3);
    const secondShelf = booksData.slice(3, 5);
    const thirdShelf = booksData.slice(5);

    this.shelves = [firstShelf, secondShelf, thirdShelf];
  },
};
</script>

<style lang="scss"></style>
