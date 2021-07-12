<template>
  <div class="book">
    <div :class="{ 'book__inner--opened': isEditing }" class="book__inner">
      <div @click="$emit('editBook', book)" class="book__spine spine">
        <div class="spine__author">{{ getAuthorInitials }}</div>
        <div class="spine__title">{{ book.title }}</div>
      </div>
      <div class="book__cover cover">
        <div class="cover__author">{{ book.author }}</div>
        <div class="cover__title">{{ book.title }}</div>
        <div class="cover__year">{{ book.year }}</div>
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
.book {
  position: relative;
  height: 50px;
  width: 25vw;
  perspective: 50000px;

  &__inner {
    width: inherit;
    height: inherit;
    transform-style: preserve-3d;
    transform: rotate(0deg) rotateX(0deg);
    transition: 0.5s all;

    &--opened {
      transform: translate(130%, 400%) rotate(90deg) rotateX(-90deg);
    }
  }

  &__spine {
    position: absolute;
    width: inherit;
    height: inherit;
    border: 2px solid #000;
    border-radius: 5px;
    font-family: "Oswald", sans-serif;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 5px;
    text-transform: uppercase;
    background-color: gray;
    cursor: pointer;
  }

  .spine__author {
    font-weight: 700;
  }

  &__cover {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    text-align: center;
    padding: 30px 15px;
    font-family: "Oswald", sans-serif;
    position: absolute;
    width: 20vw;
    height: 25vw;
    border: 2px solid #000;
    border-radius: 5px;
    background-color: gray;
    transform: rotate(-90deg) rotateY(90deg) rotateX(0deg) translateX(10vw)
      translateZ(25vh) translateY(48px);
  }

  .cover__title {
    font-size: 30px;
  }

  .cover__author {
    font-size: 25px;
  }

  .cover__year {
    font-size: 18px;
  }
}
</style>
