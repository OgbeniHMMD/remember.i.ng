<template >
  <div
    class="d-flex justify-content-center align-items-center text-center min-vh-100 border-dark border-bottom m-0 my-auto"
  >
    <div>
      <logo />
      <h1 class="display-1 text-secondary">remember.i.ng</h1>
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
