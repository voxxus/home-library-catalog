<template>
  <div id="app">
    <app-list :items="shelves">
      <template #items="{ item: books }">
        <app-book-shelf>
          <app-list :items="books">
            <template #items="{ item: book }">
              <app-book @editBook="editBook" :book="book" />
            </template>
          </app-list>
        </app-book-shelf>
      </template>
    </app-list>

    <app-book-form
      v-if="showBookInfo"
      @saveBookInfo="saveBookInfo"
      @closeBookInfo="closeBookInfo"
      :show-book-form="showBookInfo"
      :book-info="bookInfo"
      :edit-mode="editMode"
    />
  </div>
</template>

<script>
import booksData from "./mock/books.json";
import AppList from "@/components/AppList";
import AppBookShelf from "@/components/AppBookShelf";
import AppBook from "@/components/AppBook";
import AppBookForm from "@/components/AppBookInfo";

export default {
  name: "App",
  components: {
    AppList,
    AppBookShelf,
    AppBook,
    AppBookForm,
  },
  data() {
    return {
      shelves: null,
      showBookInfo: false,
      bookInfo: null,
      editMode: false,
    };
  },
  created() {
    const firstShelf = booksData.slice(0, 3);
    const secondShelf = booksData.slice(3, 5);
    const thirdShelf = booksData.slice(5);

    this.shelves = [firstShelf, secondShelf, thirdShelf];
  },
  methods: {
    editBook(book) {
      this.editMode = true;
      this.showBookInfo = true;
      this.bookInfo = book;
    },
    saveBookInfo(book) {
      this.shelves.forEach((shelf) => {
        const index = shelf.findIndex((item) => item.id === book.id);
        if (index !== -1) {
          shelf.splice(index, 1, book);
        }
      });
      this.closeBookInfo();
    },
    closeBookInfo() {
      this.showBookInfo = false;
      this.bookInfo = null;
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/style";
</style>
