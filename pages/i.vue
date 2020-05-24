<template>
  <div>
    <div class="container py-4">
      <facebook-loader v-if="!article" :speed="3" primaryColor="#cccccc"></facebook-loader>

      <div v-else>
        <header class="text-center">
          <h1 class="mb-3">{{article.attributes.title ? article.attributes.title : "*No title*"}}</h1>
          <h3
            class="mb-5 text-muted"
          >{{article.attributes.snippet ? article.attributes.snippet : "*No snippet*"}}</h3>
        </header>
        <article v-html="$md.render(article.body)" class="markdown lead"></article>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import frontMatter from "front-matter";
import { FacebookLoader } from "vue-content-loader";
// Or: InstagramLoader | CodeLoader | ListLoader | BulletListLoader

export default {
  layout: "blog",
  components: {
    FacebookLoader
  },
  data: function() {
    return {
      article: null
    };
  },
  head() {
    try {
      return {
        title: `${this.article.attributes.title} - ${process.env.name}`
      };
    } catch (error) {}
  },
  created() {
    axios
      .get(
        `${process.env.bloggerURL}/${
          process.env.bloggerID
        }/posts/${this.$route.hash.slice(2)}`,
        {
          params: {
            key: process.env.bloggerKEY
          }
        }
      )
      .then(response => (this.article = frontMatter(response.data.content)))
      .catch(error => $nuxt.error({ message: error.message }));
  }
};
</script>
