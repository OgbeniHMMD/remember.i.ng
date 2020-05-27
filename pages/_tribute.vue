<template>
  <div>
    <div class="container py-4">
      <the-spinner v-if="!post" />

      <div v-else>
        <header class="text-center">
          <h1 class="mb-3">{{post.attributes.title ? post.attributes.title : "*No title*"}}</h1>
          <h3
            class="mb-5 text-muted"
          >{{post.attributes.snippet ? post.attributes.snippet : "*No snippet*"}}</h3>
        </header>
        <article v-html="$md.render(post.body)" class="markdown lead"></article>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import bloggerJSON from "~/.env/blogger.json";
import frontMatter from "front-matter";
import TheSpinner from "~/components/TheSpinner.vue";

export default {
  layout: "blog",
  components: {
    TheSpinner
  },
  data: function() {
    return {
      post: ""
    };
  },
  head() {
    try {
      return {
        title: `${this.post.attributes.title} - ${process.env.name}`
      };
    } catch (error) {}
  },
  created() {
    // fetch data from Blogger
    const blogger = bloggerJSON;
    const blogId = this.$route.params.tribute;
    const URL = `${blogger.uri}/blogs/${blogger.id}/posts/${blogId}`;
    axios
      .get(URL, {
        params: {
          key: blogger.key
        }
      })
      .then(response => (this.post = frontMatter(response.data.content)))
      .catch(error => $nuxt.error({ message: error.message }));
  }
};
</script>