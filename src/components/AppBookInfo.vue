<template>
  <div class="outer">
    <div class="book-info">
      <div class="book-info__wrapper">
        <form @submit.prevent="checkForm" class="form">
          <app-input
            v-model.trim="editingBookData.author.lastName"
            :required="true"
            input-title="Фамилия автора"
            input-placeholder="Введите фамилию автора"
            input-type="text"
          />

          <app-input
            v-model.trim="editingBookData.author.firstName"
            :required="true"
            input-title="Имя автора"
            input-placeholder="Введите имя автора"
            input-type="text"
          />

          <app-input
            v-model.trim="editingBookData.author.secondName"
            :required="false"
            input-title="Отчество автора"
            input-placeholder="Введите отчество автора"
            input-type="text"
          />

          <app-input
            v-model.trim="editingBookData.title"
            :required="true"
            input-title="Название книги"
            input-placeholder="Введите название книги"
            input-type="text"
          />

          <app-input
            v-model.trim="editingBookData.pages"
            input-title="Количество страниц"
            input-placeholder="Введите количество страниц"
            input-type="number"
          />

          <app-input
            v-model.trim="editingBookData.year"
            input-title="Год написания"
            input-placeholder="Введите год написания"
            input-type="number"
          />

          <div class="book-info__controls">
            <button type="submit" class="button form__btn-save">
              Сохранить
            </button>
            <button
              type="button"
              class="button form__btn-cancel"
              @click="$emit('closeBookInfo')"
            >
              Отмена
            </button>
            <button
              v-if="editMode"
              type="button"
              class="button form__btn-delete"
              @click="$emit('confirmDeleteBook', editingBookData)"
            >
              Удалить
            </button>
          </div>
        </form>
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
      default: () => ({}),
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
      this.editingBookData = JSON.parse(JSON.stringify(this.bookInfo));
    } else {
      this.editingBookData = {
        id: this.nextBookId,
        author: {
          lastName: "",
          firstName: "",
          secondName: "",
        },
        title: "",
        pages: "",
        year: "",
      };
    }
  },

  methods: {
    checkForm() {
      if (this.editMode) this.$emit("saveBookInfo", this.editingBookData);
      else this.$emit("createBook", this.editingBookData);
    },
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
  z-index: 10;
}

.book-info {
  max-width: 30%;
  height: 100vh;
  position: fixed;
  background-color: aliceblue;
  border-left: 1px solid #000;
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
      min-width: 40%;
      margin-bottom: 25px;
      align-content: start;
    }
  }
}
</style>
