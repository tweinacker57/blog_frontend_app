<template>

  <div class="posts-edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit a Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label> 
        <input type="text" class="form-control" v-model="post.title">
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="post.body">
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="post.image">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: {},
      errors: [],
    };
  },
  created: function () {
    console.log("in the created");
    this.getPostData;
  },
  methods: {
    submit: function () {
      var params = {
        title: this.post.title,
        body: this.post.body,
        image: this.post.image,
      };
      axios
        .patch("/api/posts" + this.$router.params.id, params)
        .then((response) => {
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
  getPostData: function () {
    axios.get("/api/posts" + this.$router.params.id).then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
};
</script>