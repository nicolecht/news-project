<template>
  <Search />
  <Articles @delete-article="deleteArticle" :articles="articles" />
</template>

<script>
import Search from "../components/Search.vue";
import Articles from "../components/Articles.vue";
import axios from "axios";

export default {
  name: "HomePage",
  components: {
    Search,
    Articles,
  },
  data() {
    return { articles: [] };
  },

  methods: {
    async deleteArticle(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/articles/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.articles = this.articles.filter(
              (article) => article.id !== id
            ))
          : alert("Error Deleting Article");
      }
    },
    // async fetchArticles() {
    //   const res = await fetch("api/articles");
    //   const data = await res.json();
    //   return data;
    // },
    // async fetchArticle(id) {
    //   const res = await fetch(`api/articless/${id}`);
    //   const data = await res.json();
    //   return data;
    // },
    async fetchArticles() {
      try {
        const url = `https://newsapi.org/v2/top-headlines?country=us&apiKey=c0316d3b021a4cc2b428f7d5d9d6e0f1`;
        const response = await axios.get(url);
        const articles = response.data.articles;
        this.articles = articles.map((article) => ({
          title: article.title,
          description: article.description,
        }));

        await fetch("/api/articles", {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(articles),
        });
      } catch (err) {
        if (err.response) {
          // client received an error response (5xx, 4xx)
          console.log("Server Error:", err);
        } else if (err.request) {
          // client never received a response, or request never left
          console.log("Network Error:", err);
        } else {
          console.log("Client Error:", err);
        }
      }
    },
  },
  mounted() {
    this.fetchArticles();
  },
};
</script>
