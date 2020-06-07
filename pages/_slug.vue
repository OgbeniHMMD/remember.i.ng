<template>
  <section class="container py-4">
    <header class="text-center">
      <h1 class="mb-3">{{ tribute.title ? tribute.title : "*No title*" }}</h1>
      <h3 class="mb-4 text-muted">{{tribute.snippet ? tribute.snippet : "*No snippet*"}}</h3>
    </header>

    <nuxt-content :document="tribute" class="mt-4 markdown lead" />

    <div class="mt-4">
      <a
        target="_blank"
        class="text-muted"
        title="Edit this page on GitHub"
        :href="`${github.url}/edit/${github.branch}/content/tribute/${tribute.slug}.md`"
      >
        Edit this page on GitHub
        <i class="las la-external-link-alt mr-3"></i>
      </a>
    </div>
  </section>
</template>


<script>
export default {
  data: function() {
    return {
      // github repository
      github: {
        branch: "master",
        url: "https://github.com/OgbeniHMMD/remember.i.ng"
      }
    };
  },
  head() {
    try {
      return {
        title: this.tribute.title + " - " + process.env.app.name,
        meta: [
          {
            hid: "description",
            name: "description",
            content: this.tribute.description
          },
          // Open Graph
          {
            hid: "og:title",
            property: "og:title",
            content: this.tribute.title
          },
          {
            hid: "og:description",
            property: "og:description",
            content: this.tribute.description
          },
          // Twitter Card
          {
            hid: "twitter:title",
            name: "twitter:title",
            content: this.tribute.title
          },
          {
            hid: "twitter:description",
            name: "twitter:description",
            content: this.tribute.description
          }
        ]
      };
    } catch (error) {}
  },

  async asyncData({ $content, params, error }) {
    let tribute;
    const slug = "tributes/" + params.slug;

    try {
      tribute = await $content(slug).fetch();
    } catch (e) {
      return error({ statusCode: 404, message: "Page not found" });
    }

    return {
      tribute
    };
  }
};
</script>