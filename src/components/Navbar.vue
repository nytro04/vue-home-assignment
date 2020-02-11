<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-info">
    <router-link class="navbar-brand" to="/">AFG</router-link>
    <button
      type="button"
      class="navbar-toggler"
      data-toggle="collapse"
      data-target="#assignmentOne"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="assignmentOne">
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <router-link to="/services" class="nav-link">Services</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/about" class="nav-link">About</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/contact" class="nav-link">Contact</router-link>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar"
};
</script>

<style lang="scss" scoped></style>
