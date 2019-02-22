<template>
  <div class="posts-index">
    <h1>All Posts</h1>

    <div class="row">
      <div class="col-md-4" v-for="post in posts ">
        <div class="card">
        <router-link v-bind:to="'/posts/' + post.id">
        <img v-bind:src="post.image" v-bind:alt="post.title">
        </router-link>
        
          <div class="card-body">
            <h5 class="class-title">
              <h2>{{ post.title }}</h2> 
            </h5>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>

<style>
  img{
    width: 250px;

  }
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      posts: [],
      currentPost: {}
    };
  },
  created: function() {
    axios.get("/api/posts")
      .then(response => {
        this.posts = response.data;
      });
  },
  methods: {}
};
</script>