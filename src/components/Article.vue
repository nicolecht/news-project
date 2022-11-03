<template>
  <th>{{ article.title }}</th>
  <td>{{ article.description }}</td>
  <td>
    <button class="btn btn-success">View News</button>
    <button class="btn btn-info mx-2">Edit News</button>
    <button @click="$emit('delete-article', article.id)" class="btn btn-danger">
      Delete News
    </button>
  </td>
</template>

<script>
export default {
  name: "Article",
  props: {
    article: Object,
  },
};
</script>
