<template>
  <section class="container py-4">
    <h2 class="text-center text-secondary mb-5">{{ appSlogan }}</h2>

    <article
      :key="tribute.slug"
      v-for="tribute in tributes"
      class="d-flex flex-column flex-md-row position-relative mb-5"
    >
      <img :src="tribute.thumbnail ? tribute.thumbnail : defaultThumbnail" class="thumb" />

      <div class="mt-3 mt-md-0 ml-md-4">
        <a :href="`/${tribute.slug}`" class="stretched-link">
          <h1 class="text-dark mt-0 mb-2">{{ tribute.title ? tribute.title: "*No title*" }}</h1>
        </a>
        <div
          class="text-muted lead mt-2 mt-md-3"
        >{{ tribute.snippet ? tribute.snippet: "*No snippet*" }}</div>
      </div>
    </article>
  </section>
</template>


<script>
export default {
  data() {
    return {
      defaultThumbnail: "/img/default-thumbnail.jpg",
      appSlogan: process.env.app.slogan
    };
  },

  async asyncData({ $content, params, error }) {
    let tributes;

    try {
      tributes = await $content("tributes")
        .only(["title", "slug", "thumbnail", "createdAt", "snippet"])
        .fetch();
    } catch (e) {
      return error({ statusCode: 404, message: "Page not found" });
    }

    return {
      tributes
    };
  }
};
</script>