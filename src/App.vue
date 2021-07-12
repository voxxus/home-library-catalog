<template>
  <div id="app">
    <app-list :items="shelves">
      <template #items="{ item: books }">
        <app-book-shelf @addBook="addBook(books)" :books="books">
          <app-list v-if="books.length" :items="books">
            <template #items="{ item: book }">
              <app-book
                @editBook="editBook"
                :editing-book-info="bookInfo"
                :book="book"
              />
            </template>
          </app-list>
          <div v-else class="message">В этой полке книг нет :(</div>
        </app-book-shelf>
      </template>
    </app-list>

    <app-book-form
      v-if="showBookInfo"
      @createBook="createBook"
      @saveBookInfo="saveBookInfo"
      @closeBookInfo="closeBookInfo"
      @confirmDeleteBook="confirmDeleteBook"
      :show-book-form="showBookInfo"
      :book-info="bookInfo"
      :edit-mode="editMode"
      :next-book-id="nextBookId"
    />

    <app-modal-window v-if="showModalWindow">
      <template #title>Удаление книги</template>
      <template #content>
        <p class="modal-text">
          Вы действительно хотите удалить книгу '{{ bookToDelete.title }}'?
        </p>
        <div class="modal-controls">
          <button
            @click="deleteBook(bookToDelete)"
            class="button modal-btn-delete"
          >
            Удалить
          </button>
          <button @click="closeModalWindow" class="button modal-btn-delete">
            Отмена
          </button>
        </div>
      </template>
    </app-modal-window>
  </div>
</template>

<script>
import booksData from "./mock/books.json";
import AppList from "@/components/AppList";
import AppBookShelf from "@/components/AppBookShelf";
import AppBook from "@/components/AppBook";
import AppBookForm from "@/components/AppBookInfo";
import AppModalWindow from "@/components/AppModalWindow";

export default {
  name: "App",

  components: {
    AppModalWindow,
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
      nextBookId: null,
      currentShelf: null,
      showModalWindow: false,
      bookToDelete: null,
    };
  },

  created() {
    document.title = "Каталог домашней библиотеки";

    const firstShelf = booksData.slice(0, 3);
    const secondShelf = booksData.slice(3, 4);
    const thirdShelf = booksData.slice(4);

    this.shelves = [firstShelf, secondShelf, thirdShelf];
  },

  methods: {
    addBook(shelf) {
      this.getNextBookId();
      this.currentShelf = shelf;
      this.showBookInfo = true;
    },

    editBook(book) {
      this.editMode = true;
      this.showBookInfo = true;
      this.bookInfo = book;
    },

    createBook(book) {
      this.currentShelf.push(book);
      this.closeBookInfo();
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

    confirmDeleteBook(book) {
      this.showModalWindow = true;
      this.bookToDelete = book;
    },

    deleteBook(book) {
      this.shelves.forEach((shelf) => {
        const index = shelf.findIndex((item) => item.id === book.id);
        if (index !== -1) {
          shelf.splice(index, 1);
        }
      });
      this.closeBookInfo();
      this.closeModalWindow();
    },

    closeBookInfo() {
      this.showBookInfo = false;
      this.bookInfo = null;
      this.nextBookId = null;
      this.currentShelf = null;
      this.editMode = false;
    },

    getNextBookId() {
      const allBooks = [];
      this.shelves.forEach((shelf) => allBooks.push(...shelf));
      allBooks.sort((a, b) => a.id - b.id);
      this.nextBookId = allBooks[allBooks.length - 1].id + 1;
    },

    closeModalWindow() {
      this.showModalWindow = false;
      this.bookToDelete = false;
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/style";

.modal-text {
  margin-bottom: 15px;
}

.modal-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.message {
  margin: 25px 0;
  text-align: center;
}
</style>
