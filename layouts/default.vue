<template>
  <div>
    <the-header />
    <nuxt />
    <the-footer />
  </div>
</template>

<script>
import TheHeader from "~/layouts/partials/header.vue";
import TheFooter from "~/layouts/partials/footer.vue";

export default {
  components: {
    TheHeader,
    TheFooter
  }
};
</script>

<style lang="scss">
//Import SCSS files importer
@import "~/assets/styles/importer.scss";
</style>
