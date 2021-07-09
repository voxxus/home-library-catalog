<template>
  <div class="outer">
    <div class="book-info">
      <div class="book-info__wrapper">
        <app-input
          :input-title="'Автор'"
          :input-placeholder="'Введите имя автора'"
          :input-type="'text'"
          v-model="editingBookData.author"
        />
        <app-input
          :input-title="'Название книги'"
          :input-placeholder="'Введите название книги'"
          :input-type="'text'"
          v-model="editingBookData.title"
        />
        <app-input
          :input-title="'Количество страниц'"
          :input-placeholder="'Введите количество страниц'"
          :input-type="'number'"
          v-model="editingBookData.pages"
        />
        <app-input
          :input-title="'Год написания'"
          :input-placeholder="'Введите год написания'"
          :input-type="'number'"
          v-model="editingBookData.year"
        />

        <div class="book-info__controls">
          <button
            v-if="editMode"
            @click="$emit('saveBookInfo', editingBookData)"
            class="button form__btn-save"
          >
            Сохранить
          </button>
          <button
            v-else
            @click="$emit('createBook', editingBookData)"
            class="button form__btn-save"
          >
            Сохранить
          </button>

          <button
            @click="$emit('closeBookInfo')"
            class="button form__btn-cancel"
          >
            Отмена
          </button>
          <button
            v-if="editMode"
            @click="$emit('confirmDeleteBook', editingBookData)"
            class="button form__btn-delete"
          >
            Удалить
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppInput from "@/components/AppInput";

export default {
  name: "AppBookInfo",
  components: {
    AppInput,
  },
  props: {
    showBookForm: {
      type: Boolean,
      default: false,
    },
    bookInfo: {
      type: Object,
      default: () => {},
    },
    editMode: {
      type: Boolean,
      default: false,
    },
    nextBookId: {
      type: Number,
      default: -1,
    },
  },
  data() {
    return {
      editingBookData: {},
    };
  },
  created() {
    if (this.editMode) {
      Object.assign(this.editingBookData, this.bookInfo);
    } else {
      this.editingBookData = {
        id: this.nextBookId,
        author: "",
        title: "",
        pages: "",
        year: "",
      };
    }
  },
};
</script>

<style lang="scss" scoped>
.outer {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  right: 0;
  background-color: rgba(255, 255, 255, 0.39);
  z-index: 10;
}

.book-info {
  max-width: 30%;
  height: 100vh;
  position: absolute;
  background-color: aliceblue;
  top: 0;
  right: 0;
  z-index: 100;

  &__wrapper {
    padding: 20px 50px;
  }

  &__controls {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;

    & > .button {
      //flex: 50%;
      min-width: 40%;
      margin-bottom: 25px;
      align-content: start;
    }
  }
}
</style>
