<template>
  <div class="posts-new">
    <h1>New Post</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      <div>
        Title: <input v-model="newPostTitle">
      </div>
      <div>
        Body: <input v-model="newPostChef">
      </div> 
      <div>
        Image URL: <input v-model="newPostImage_url">
      </div>

      <input type="submit" value="Create" class="btn btn-warning">
    </form>
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      newPostTitle: "",
      newPostBody: "",
      newPostImage_url: "",
      errors: []
    };
  },

  created: function() {},
  methods: {
    submit: function() {
      console.log("Create the Recipe....");
      var params = {
                    title: this.newPostTitle,
                    body: this.newPostBody,
                    image_url: this.newPostImage_url
                    };
      axios.post("/api/posts", params)
        .then(response => {
          console.log("Success", response.data);
          this.$router.push("/");
        }).catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
}
</script>