<template>
  <div>
    <div class="d-flex justify-content-center align-items-center min-vh-100 my-auto">
      <div>
        <div class="display-3 text-center">{{error.statusCode}} Error!</div>
        <div class="display-4 text-center">{{error.message}}</div>

        <div class="display-1 text-center">
          <i class="las la-frown"></i>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    error: {
      type: Object,
      default: null,
      statusCode: ""
    }
  },
  head() {
    return {
      title: `${this.error.statusCode} error - ${process.env.name}`
    };
  }
};
</script>