<template>
  <div>
    <div class="container py-4">
      <the-spinner v-if="!post" />

      <div v-else>
        <header class="text-center">
          <h1 class="mb-3">{{post.attributes.title ? post.attributes.title : "*No title*"}}</h1>
          <h3
            class="mb-4 text-muted"
          >{{post.attributes.snippet ? post.attributes.snippet : "*No snippet*"}}</h3>
        </header>
        <article v-html="$md.render(post.body)" class="markdown lead"></article>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import frontMatter from "front-matter";
import slugsJSON from "~/assets/redirects.json";
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
        title: `${this.post.attributes.title} - ${process.env.app.name}`
      };
    } catch (error) {}
  },
  created() {
    // fetch data from Blogger
    const blogger = process.env.blogger;

    // convert slug to blog Id if it exist
    let postId = this.$route.params.tribute;
    const postSlug = slugsJSON.find(item => item.slug === postId);
    postId = postSlug ? postSlug.id : postId;

    const URL = `${blogger.uri}/blogs/${blogger.id}/posts/${postId}`;
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