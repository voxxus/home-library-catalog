<template>
  <div class="book">
    <div
      @click="$emit('editBook', book)"
      :class="{ 'spine-anim': isEditing }"
      class="book__spine spine"
    >
      <div class="spine__author">
        {{ getAuthorInitials }}
      </div>
      <div class="spine__title">
        {{ book.title }}
      </div>
    </div>
    <!--    <div v-if="isEditing" class="book__cover cover">-->
    <!--      <div class="cover__author">{{ book.author }}</div>-->
    <!--      <div class="cover__title">{{ book.title }}</div>-->
    <!--      <div class="cover__year">{{ book.year }}</div>-->
    <!--    </div>-->
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
    editingBookInfo: {
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

    isEditing() {
      return this.book.id === this.editingBookInfo?.id;
    },
  },
};
</script>

<style lang="scss" scoped>
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
  transition: 1s all;

  &__author {
    font-weight: 700;
  }
}

.spine-anim {
  transform: translate(130%, 500%) rotate(90deg);
}
</style>
