<template>
  <div class="container py-4">
    <div v-if="spinner" class="text-center display-1">
      <i class="las la-spinner la-spin text-primary m-5"></i>
    </div>

    <div v-if="!spinner">
      <header class="text-center">
        <h1 class="mb-3">{{ post.title.split(':')[0] }}</h1>
        <h3 class="mb-5">{{ post.title.split(':')[1] }}</h3>
      </header>

      <div v-html="post.content" class="lead"></div>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  layout: "blog",
  data: function() {
    return {
      spinner: true,
      post: []
    };
  },
  head() {
    try {
      return {
        title: `${this.post.title.split(":")[0]} - ${process.env.name}`
      };
    } catch (error) {}
  },
  created() {
    axios
      .get(
        `https://www.googleapis.com/blogger/v3/blogs/${process.env.bloggerId}/posts/${this.$route.query.ute}?key=${process.env.bloggerKey}`
      )
      .then(response => {
        this.spinner = false;
        this.post = response.data;
      })
      .catch(e => {
        $nuxt.error({ message: e.message });
      });
  }
};
</script>
