<template >
  <header
    class="navbar navbar-expand-md navbar-light bg-s border-secondary border-bottom p-1 px-sm-4"
  >
    <a class="navbar-brand text-dark lead p-0" href="/">
      <i class="las la-seedling la-2x"></i>
      <span>{{ appName }}</span>
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

    <nav id="navbar1" class="collapse navbar-collapse" :class="(toggle.navbar ? 'show' : 'hide')">
      <form
        class="input-group input-group-sm nav-item border rounded col-md-7 ml-auto mt-2 mt-md-0 px-0"
      >
        <input
          type="search"
          class="form-control border-0 shadow-none"
          placeholder="Search"
          aria-label="Search"
          aria-describedby="button-addon1"
        />
        <div class="input-group-append">
          <button class="btn bg-white shadow-none" type="button" id="button-addon1">
            <i class="las la-search text-secondary"></i>
          </button>
        </div>
      </form>
    </nav>
  </header>
</template>

<script>
export default {
  data: function() {
    return {
      appName: process.env.app.name,
      toggle: { navbar: false, dropDown1: false }
    };
  }
};
</script>