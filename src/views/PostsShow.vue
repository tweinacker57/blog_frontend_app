<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <h1>Title: {{ post.title }}</h1>
    <h1>Body: {{ post.body }}</h1>
    <h1>Image: {{ post.image }}</h1>
    <br>
     <router-link v-bind:to="`/posts/${post.id}/edit`">Edit</router-link>
    <button v-on:click="postsDestroy()">Delete</button>
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
      console.log(this.$router.params.id);
      axios.get("/api/posts/" + this.$router.params.id).then((response) => {
        console.log(response.data);
        this.postsShow = response.data;
      });
    },
  },
  // postsDestroy: function () {
  //   console.log("destroying post");
  //   axios.delete(`/api/posts/${this.post.id}`).then((response) => {
  //     console.log(response.data);
  //     this.$router.push("/posts");
  //   });
  // },
};
</script>
