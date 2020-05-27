<template >
  <div class="container py-4">
    <h2 class="text-center text-secondary mb-5">{{ appDescription }}</h2>

    <the-spinner v-if="!posts" />

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
        <a :href="'/' + post.id" class="stretched-link">
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
import TheSpinner from "~/components/TheSpinner.vue";

export default {
  components: {
    TheSpinner
  },
  data() {
    return {
      posts: "",
      appDescription: process.env.app.slogan
    };
  },
  async created() {
    // fetch data from Blogger
    const blogger = process.env.blogger;
    const URL = `${blogger.uri}/blogs/${blogger.id}/posts/`;

    await axios
      .get(URL, {
        params: {
          key: blogger.key,
          fetchImages: false,
          replies: false
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