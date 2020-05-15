<template >
  <div class="container py-4">
    <div class="text-center text-secondary h2 mb-5">Tributes To The Good, The Bad And The Ugly</div>

    <div v-if="spinner" class="text-center display-1">
      <i class="las la-spinner la-spin text-primary m-5"></i>
    </div>

    <div v-if="!spinner">
      <article
        :key="post.id"
        class="d-flex flex-column flex-md-row position-relative mb-5"
        v-for="post in posts.items"
      >
        <img :src="post.images? post.images[0].url : '/thumb.jpg'" class="thumb" />
        <div class="mt-3 mt-md-0 ml-md-4">
          <a :href="'/trib?ute=' + post.id" class="stretched-link">
            <h1 class="text-dark mt-0 mb-2">{{ post.title.split(':')[0] }}</h1>
          </a>
          <div class="text-muted lead mt-2 mt-md-3">{{ post.title.split(':')[1] }}</div>
        </div>
      </article>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      posts: [],
      errors: [],
      spinner: true
    };
  },
  head() {
    return {
      title: `${process.env.name} - ${process.env.description}`
    };
  },
  created() {
    axios
      .get(
        `https://www.googleapis.com/blogger/v3/blogs/${process.env.bloggerId}/posts?key=${process.env.bloggerKey}&fetchImages=true`
      )
      .then(response => {
        this.spinner = false;
        this.posts = response.data;
      })
      .catch(e => {
        $nuxt.error({ message: e.message });
      });
  }
};
</script>