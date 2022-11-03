<template>
  <b-table
    id="my-table"
    :items="items"
    :per-page="perPage"
    :current-page="currentPage"
    small
    class="table table-striped table-hover table-bordered align-middle"
  >
    <p class="mt-3">Current Page: {{ currentPage }}</p>
    <thead>
      <tr>
        <th class="w-25">Title</th>
        <th class="w-50">Description</th>
        <th class="w-25">Options</th>
      </tr>
    </thead>
    <tbody class="">
      <tr :key="article.id" v-for="article in articles">
        <Article
          @delete-article="$emit('delete-article', article.id)"
          :article="article"
        />
      </tr>
    </tbody>
  </b-table>
</template>

<script>
import Article from "./Article.vue";

export default {
  data() {
    return {
      perPage: 3,
      currentPage: 1,
      items: [
        { id: 1, first_name: "Fred", last_name: "Flintstone" },
        { id: 2, first_name: "Wilma", last_name: "Flintstone" },
        { id: 3, first_name: "Barney", last_name: "Rubble" },
        { id: 4, first_name: "Betty", last_name: "Rubble" },
        { id: 5, first_name: "Pebbles", last_name: "Flintstone" },
        { id: 6, first_name: "Bamm Bamm", last_name: "Rubble" },
        { id: 7, first_name: "The Great", last_name: "Gazzoo" },
        { id: 8, first_name: "Rockhead", last_name: "Slate" },
        { id: 9, first_name: "Pearl", last_name: "Slaghoople" },
      ],
    };
  },
  computed: {
    rows() {
      return this.items.length;
    },
  },
  name: "Articles",
  props: {
    articles: Array,
  },
  components: {
    Article,
  },
  emits: ["delete-article"],
};
</script>
