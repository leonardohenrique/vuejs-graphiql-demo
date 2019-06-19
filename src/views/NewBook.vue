<template>
  <div>
    <h1>New Books</h1>
    <form @submit.prevent="addBook">
      <div class="form-group">
        <label for="title">Title</label>
        <input
          type="text"
          class="form-control"
          id="title"
          placeholder="Enter title"
          v-model="book.title"
        >
      </div>
      <div class="form-group">
        <label for="author_id">Author</label>
        <input
          type="text"
          class="form-control"
          id="author_id"
          placeholder="Enter author"
          v-model="book.authorId"
        >
      </div>
      <div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="checkbox"
            id="genre1"
            value="1"
            v-model="book.genreIds"
          >
          <label class="form-check-label" for="genre1">Fantasy</label>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="checkbox"
            id="genre2"
            value="2"
            v-model="book.genreIds"
          >
          <label class="form-check-label" for="genre2">Classics</label>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="checkbox"
            id="genre3"
            value="3"
            v-model="book.genreIds"
          >
          <label class="form-check-label" for="genre3">Horror</label>
        </div>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  data() {
    return {
      book: {
        title: "The Silmarillion",
        authorId: 1,
        genreIds: [1, 2]
      }
    };
  },
  methods: {
    addBook() {
      this.$apollo
        .mutate({
          mutation: gql`
            mutation($title: String!, $authorId: ID!, $genreIds: [ID]) {
              addBook(
                input: {
                  title: $title
                  authorId: $authorId
                  genreIds: $genreIds
                }
              ) {
                id
              }
            }
          `,
          variables: this.book
        })
        .then(mutationResult => {
          this.$router.push({
            name: "book",
            params: { id: mutationResult.data.addBook.id }
          });
        });
    }
  }
};
</script>
