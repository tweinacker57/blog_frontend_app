<template>
  <div class="posts-index">
    <h1>{{ message }}</h1>
    <div v-for="post in posts">
      <p>{{ post.title }}</p>
      <router-link v-bind:to="'/posts/' + post.id">
      </router-link>
    </div>  
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Posts",
      posts: [],
    };
  },
  created: function () {
    this.postsIndex();
  },
  methods: {
    postsIndex: function () {
      axios.get("/api/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>