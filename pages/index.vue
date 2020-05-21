<template >
  <div class="container py-4">
    <div class="text-center text-secondary h2 mb-5">{{ appDescription }}</div>

    <div v-if="!posts" class="text-center display-1">
      <i class="las la-spinner la-spin text-primary m-5"></i>
    </div>

    <article
      v-else
      :key="post.id"
      v-for="post in posts.items"
      class="d-flex flex-column flex-md-row position-relative mb-5"
    >
      <img
        :src=" getAttributes(post).thumbnail? getAttributes(post).thumbnail: '/thumb.jpg'"
        class="thumb"
      />
      <div class="mt-3 mt-md-0 ml-md-4">
        <a :href="'/trib?ute=' + post.id" class="stretched-link">
          <h1
            class="text-dark mt-0 mb-2"
          >{{ getAttributes(post).title? getAttributes(post).title: "*No title*" }}</h1>
        </a>
        <div
          class="text-muted lead mt-2 mt-md-3"
        >{{ getAttributes(post).snippet? getAttributes(post).snippet: "*No snippet*" }}</div>
      </div>
    </article>
  </div>
</template>

<script>
import axios from "axios";
import frontMatter from "front-matter";

export default {
  data() {
    return {
      posts: null,
      appDescription: process.env.description
    };
  },
  head() {
    return {
      title: `${process.env.name} - ${process.env.description}`
    };
  },
  created() {
    axios
      .get(`${process.env.bloggerURL}/${process.env.bloggerID}/posts`, {
        params: {
          key: process.env.bloggerKEY,
          fetchImages: true
        }
      })
      .then(response => (this.posts = response.data))
      .catch(error => $nuxt.error({ message: error.message }));
  },
  methods: {
    getAttributes(rawArticle) {
      try {
        return frontMatter(rawArticle.content).attributes;
      } catch (error) {}
    }
  }
};
</script>