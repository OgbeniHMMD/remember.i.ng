<template >
  <div class="container text-center min-vh-100 m-0 my-auto">
    <logo />
    <h1 class="text-secondary">remember.i.ng</h1>
    <h2 class="h1 text-dark">My Collection Of Tribute Pages</h2>
    <div class="mt-4">
      <a
        href="https://nuxtjs.org/"
        target="_blank"
        class="btn btn-lg btn-outline-primary mr-4"
      >Documentation</a>
      <a
        href="https://github.com/nuxt/nuxt.js"
        target="_blank"
        class="btn btn-lg btn-outline-dark mr-4"
      >GitHub</a>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  components: {
    Logo
  }
};
</script>
