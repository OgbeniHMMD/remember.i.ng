<template >
  <div class="container py-4">
    <div class="text-center text-secondary h2 mb-5">Tributes To The Good, The Bad And The Ugly</div>

    <div v-if="spinner" class="text-center h1">
      <i class="las la-spinner la-spin text-primary m-5"></i>
    </div>

    <div v-if="!spinner">
      <article
        :key="post.id"
        class="d-flex flex-column flex-md-row position-relative mb-5"
        v-for="post in posts.items"
      >
        <img
          :src="post.images? post.images[0].url : '/thumb.jpg'"
          class="thumb img-fluid mb-3 mr-md-4"
        />

        <div>
          <div>
            <a :href="'/tribute?id=' + post.id" class="stretched-link">
              <h1 class="text-dark mt-0 mb-2">{{ post.title.split(':')[0] }}</h1>
            </a>
          </div>
          <div class="text-muted lead mt-3">{{ post.title.split(':')[1] }}</div>
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

<style lang="scss">
.thumb {
  max-width: 320;
}
</style>