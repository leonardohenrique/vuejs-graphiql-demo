<template>
  <div v-if="book">
    <h1>{{ book.title }}</h1>
    <h3>{{ book.author.name }}</h3>
    Genres: {{ book.genres.map(g => g.name).join(', ') }}
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  apollo: {
    book: {
      query: gql`
        query bookQuery($id: ID!) {
          book(id: $id) {
            id
            title
            author {
              name
            }
            genres {
              name
            }
          }
        }
      `,
      variables() {
        return {
          id: this.id
        };
      }
    }
  },
  props: ["id"]
};
</script>

