<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <h1>{{ header }}</h1>
      <button class="btn btn-primary">Add News</button>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    header: String,
  },
};
</script>
