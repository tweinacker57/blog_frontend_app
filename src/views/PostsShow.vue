<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <h1>Title: {{ post.title }}</h1>
    <h1>Body: {{ post.body }}</h1>
    <h1>Image: {{ post.image }}</h1>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      post: {},
    };
  },
  created: function () {
    this.postsShow();
  },
  methods: {
    postsShow: function () {
      console.log("in the show..");
      console.log(this.$route.params.id);
      axios.get("/api/posts/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.postsShow = response.data;
      });
    },
  },
};
</script>
