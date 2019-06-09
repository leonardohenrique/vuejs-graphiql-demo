<template>
  <div>
    <h1>Books</h1>
    <table class="table table-striped table-bordered">
      <thead>
        <tr>
          <th>ID</th>
          <th>Title</th>
          <th>Author</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="book in books" :key="book.id">
          <td>{{ book.id }}</td>
          <td>{{ book.title }}</td>
          <td>{{ book.author.name }}</td>
          <td>
            <router-link :to="{ name: 'book', params: { id: book.id }}">Details</router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  apollo: {
    books: gql`
      query {
        books {
          id
          title
          author {
            name
          }
        }
      }
    `
  }
};
</script>

