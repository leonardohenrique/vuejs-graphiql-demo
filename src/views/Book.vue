<template>
  <div>
    <h1>id: {{ id }}</h1>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  apollo: {
  },
  props: ['id']
};
</script>

