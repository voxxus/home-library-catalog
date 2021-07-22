<template>
  <div class="bookshelf">
    <div class="bookshelf__controls">
      <div @click="sortBooks('author.lastName')" class="bookshelf__sort-author">
        <span class="bookshelf__sort-text">По автору</span>
        <span
          :class="{
            'bookshelf__arrow-up--active':
              this.sortDirection === 'asc' && this.sortKey === 'author',
          }"
          class="bookshelf__arrow-up"
          >&nbsp;&uarr;</span
        >
        <span
          :class="{
            'bookshelf__arrow-down--active':
              this.sortDirection === 'desc' && this.sortKey === 'author',
          }"
          class="bookshelf__arrow-down"
          >&nbsp;&darr;</span
        >
      </div>
      <div @click="sortBooks('title')" class="bookshelf__sort-title">
        <span class="bookshelf__sort-text">По названию</span>
        <span
          :class="{
            'bookshelf__arrow-up--active':
              this.sortDirection === 'asc' && this.sortKey === 'title',
          }"
          class="bookshelf__arrow-up"
          >&nbsp;&uarr;</span
        >
        <span
          :class="{
            'bookshelf__arrow-down--active':
              this.sortDirection === 'desc' && this.sortKey === 'title',
          }"
          class="bookshelf__arrow-down"
          >&nbsp;&darr;</span
        >
      </div>
      <span @click="resetSort" class="bookshelf__reset">
        Сброс сортировки
      </span>
      <span @click="$emit('addBook')" class="bookshelf__add">
        Добавить книгу
      </span>
    </div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "AppBookShelf",
  props: {
    books: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      sortKey: "author",
      sortDirection: "none",
    };
  },

  methods: {
    sortBooks(property) {
      if (this.sortKey !== property) this.sortKey = property;
      this.sortDirection = this.sortDirection === "asc" ? "desc" : "asc";

      return this.books.sort(this.sortBooksBy(property, this.sortDirection));
    },

    sortBooksBy(property, order) {
      this.sortDirection = order;

      if (property.includes(".")) {
        const properties = property.split(".");
        const [prop, nestedProp] = properties;
        return (a, b) => {
          const prevBook = a[prop][nestedProp].toLowerCase();
          const nextBook = b[prop][nestedProp].toLowerCase();
          let comparison = 0;

          if (prevBook > nextBook) comparison = 1;
          else if (prevBook < nextBook) comparison = -1;

          return order === "desc" ? comparison * -1 : comparison;
        };
      } else {
        return (a, b) => {
          const prevBook = a[property].toLowerCase();
          const nextBook = b[property].toLowerCase();
          let comparison = 0;

          if (prevBook > nextBook) comparison = 1;
          else if (prevBook < nextBook) comparison = -1;

          return order === "desc" ? comparison * -1 : comparison;
        };
      }
    },

    resetSort() {
      this.sortDirection = "none";
      this.books.sort((a, b) => a.id - b.id);
    },
  },
};
</script>

<style lang="scss" scoped>
.bookshelf {
  max-width: 30%;
  min-height: 30%;
  border: 3px solid #652121;
  background: url("../assets/images/bookshelf-bg.jpg") center center / cover
    no-repeat;
  padding: 10px 10px 0;
  transition: 0.3s all;

  &__controls {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    font-size: 15px;
    user-select: none;
    color: #fff;
  }

  &__sort-author,
  &__sort-title,
  &__reset,
  &__add {
    cursor: pointer;

    &:hover {
      text-decoration: underline;
      text-underline-offset: 2px;
    }
  }

  &__arrow-up--active {
    color: #a86c37;
  }

  &__arrow-down--active {
    color: #a86c37;
  }
}
</style>
