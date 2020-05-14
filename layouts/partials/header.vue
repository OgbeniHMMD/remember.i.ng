<template >
  <header>
    <nav
      class="navbar sticky-top navbar-expand-md navbar-light bg-white border-bottom sha dow-sm p-1 px-sm-4"
    >
      <a class="navbar-brand text-dark lead p-0" href="/">
        <i class="las la-seedling la-2x"></i>
        <span>remember.i.ng</span>
      </a>

      <button
        class="navbar-toggler lead rounded-circle"
        type="button"
        data-toggle="collapse"
        data-target="#navbar1"
        aria-controls="navbar1"
        aria-expanded="false"
        aria-label="Toggle navigation"
        @click="(toggle.navbar = !toggle.navbar)"
      >
        <i class="las la-search py-2"></i>
      </button>

      <div id="navbar1" class="collapse navbar-collapse" :class="(toggle.navbar ? 'show' : 'hide')">
        <form class="input-group nav-item border rounded col-md-7 ml-auto mt-2 mt-md-0 px-0">
          <input
            type="search"
            class="form-control border-0"
            placeholder="Search"
            aria-label="Search"
            aria-describedby="button-addon1"
          />
          <div class="input-group-append">
            <button class="btn bg-white" type="button" id="button-addon1">
              <i class="las la-search text-secondary"></i>
            </button>
          </div>
        </form>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  data: function() {
    return {
      toggle: { navbar: false, dropDown1: false }
    };
  }
};
</script>

<style lang="scss">
</style>
