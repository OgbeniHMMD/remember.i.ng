<template>
  <div>
    <div class="container py-4">
      <div v-if="!article" class="text-center display-1">
        <i class="las la-spinner la-spin text-primary m-5"></i>
      </div>

      <div v-else>
        <header class="text-center">
          <h1 class="mb-3">{{article.attributes.title ? article.attributes.title : "Untitled"}}</h1>
          <h3
            class="mb-5 text-muted"
          >{{article.attributes.snippet ? article.attributes.snippet : "- - -"}}</h3>
        </header>

        <div v-html="$md.render(article.body)" class="lead"></div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import frontMatter from "front-matter";

export default {
  layout: "blog",
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
        `https://www.googleapis.com/blogger/v3/blogs/${process.env.bloggerId}/posts/${this.$route.query.ute}?key=${process.env.bloggerKey}`
      )
      .then(response => {
        this.article = frontMatter(response.data.content);
      })
      .catch(e => $nuxt.error({ message: e.message }));
  }
};
</script>
