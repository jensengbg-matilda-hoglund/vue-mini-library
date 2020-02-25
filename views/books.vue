<template>
  <div>
    <main v-if="show" class="books">
      <book v-for="(book, index) in books" :key="index" :book="book" @book-info="toggleOverlay" />
    </main>

    <bookInfo
      v-else-if="bookInfo"
      :book="book"
      :counter="counter"
      class="overlay"
      @close-overlay="close"
      @tgl-wishlist="tglWishlist"
      @add-book="addBook"
    />
    <wishList v-else :bookCart="bookCart" @close-wishlist="close" @remove-book="remove" />
  </div>
</template>

<script>
import book from "../components/book";
import wishList from "./wishList";

import bookInfo from "./bookInfo";

export default {
  name: "books",
  components: {
    book,
    bookInfo,
    wishList
  },
  props: {
    books: Array
  },

  data: () => {
    return {
      show: true,
      bookInfo: false,
      book: {},
      bookCart: [],
      counter: 0
    };
  },
  watch: {
    bookCart() {
      localStorage.setItem("wishlist", JSON.stringify(this.bookCart));
      this.counter = this.bookCart.length;
    }
  },

  methods: {
    toggleOverlay(book) {
      this.book = book;
      this.show = false;
      this.bookInfo = true;
    },
    tglWishlist() {
      this.show = false;
      this.bookInfo = false;
    },
    close() {
      this.show = true;
    },
    addBook(book) {
      let index = this.bookCart.indexOf(book);
      if (this.bookCart[index] != book) {
        this.bookCart.push(book);
      }
    },
    remove(index) {
      this.bookCart.splice(index, 1);
    }
  }
};
</script>

<style>
.books {
  display: flex;
  width: 100%;
  flex-flow: row wrap;
  justify-content: center;
}

.overlay {
  background: linear-gradient(0deg, #222222, #222222), #eeeeee;
}
</style>
