<template>
  <div>
    <tribute-header />
    <div class="bg-light d-flex justify-content-center align-items-center">
      <tribute-body />
    </div>
    <tribute-footer />
  </div>
</template>

<script>
import TributeHeader from "~/layouts/partials/header.vue";
import TributeBody from "~/components/TributeBody.vue";
import TributeFooter from "~/layouts/partials/footer.vue";

export default {
  components: {
    TributeHeader,
    TributeBody,
    TributeFooter
  }
};
</script>
