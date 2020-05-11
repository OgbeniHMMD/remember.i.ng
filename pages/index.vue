<template>
  <div>
    <tribute-header />
    <tribute-body />
    <tribute-footer />
  </div>
</template>

<script>
import TributeHeader from "~/components/TributeHeader.vue";
import TributeBody from "~/components/TributeBody.vue";
import TributeFooter from "~/components/TributeFooter.vue";

export default {
  components: {
    TributeHeader,
    TributeBody,
    TributeFooter
  }
};
</script>
