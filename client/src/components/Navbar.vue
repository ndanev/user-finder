<template>
  <header class="header">
    <div class="container">
      <router-link to="/" class="logo">
        <img src="@/assets/github-logo.jpg" alt="Github logo" width="150" />
      </router-link>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style lang="scss">
.header {
  background: #fff;
  border-bottom: 1px solid #d9d9d9;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
  width: 100%;
}

.logo {
  text-decoration: none;
}
</style>
