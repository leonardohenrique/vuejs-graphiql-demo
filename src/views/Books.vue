<template>
  <div>books: {{ books }}</div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  apollo: {
    books: gql`
      query {
        books {
          id
          title
        }
      }
    `
  }
};
</script>

