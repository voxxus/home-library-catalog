<template>
  <div class="book">
    <div @click="$emit('editBook', book)" class="book__spine spine">
      <div class="spine__author">
        {{ getAuthorInitials }}
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
  computed: {
    getAuthorInitials() {
      const authorNameArr = this.book.author.split(" ");
      return authorNameArr
        .map((name) => {
          if (name !== authorNameArr[0]) {
            return `${name[0]}.`;
          } else {
            return name;
          }
        })
        .join(" ");
    },
  },
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;700&display=swap");

.spine {
  display: flex;
  justify-content: space-between;
  align-items: center;
  min-height: 50px;
  padding: 0 10px;
  border: 2px solid black;
  border-radius: 6px;
  background-color: gray;
  text-transform: uppercase;
  font-family: "Oswald", sans-serif;
  cursor: pointer;

  &__author {
    font-weight: 700;
  }
}
</style>
