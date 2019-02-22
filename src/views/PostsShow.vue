<template>
  <div class="posts-show">
    <img :src="post.image" :alt="post.title">
    <h1>{{ post.title }}</h1>
    <h4>Body: {{ post.body }}</h4>

    <router-link class="btn btn-info" :to=" '/posts/' + post.id + '/edit' ">Edit</router-link>
    <button class="btn btn-info" v-on:click="destroyPost()">Delete</button>

  </div>
</template>

<style></style>

<script>
var axios = require('axios');

export default {
  data: function () {
    return {
      post: {
              id: "",
              title: "",
              body: "",
              image: ""
              }
    };
  },
  created: function () {
    axios.get("/api/posts/" + this.$route.params.id )
      .then(response => {
        console.log(response.data);
        this.post = response.data;
      });
  },
  methods: {
    destroyPost: function() {
      axios.delete("/api/posts/" + this.post.id)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        });
    }
  }
}
</script>