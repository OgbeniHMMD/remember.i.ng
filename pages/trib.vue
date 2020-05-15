<template>
  <div class="container py-4">
    <div v-if="spinner" class="text-center display-1">
      <i class="las la-spinner la-spin text-primary m-5"></i>
    </div>

    <div v-if="!spinner">
      <header>
        <h1 class="mb-3">{{ post.title.split(':')[0] }}</h1>
        <h2 class="mb-5">{{ post.title.split(':')[1] }}</h2>
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
    return {
      title: this.post.title + " - OgbeniHMMD's Blog"
    };
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
