<template>
  <section>
    <BooksList :books="books" />
  </section>
</template>

<script>
import books from "./assets/childrensbooks.json";
import BooksList from "./views/books";

export default {
  components: {
    BooksList
  },
  computed: {
    books() {
      return books.books;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

html {
  font-family: "Roboto", sans-serif;
  color: white;
}
</style>
