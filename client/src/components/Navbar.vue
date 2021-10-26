<template>
  <header class="header">
    <div class="container">
      <div class="d-flex align-items-center justify-content-between">
        <router-link to="/" class="logo">
          <img src="@/assets/github-logo.jpg" alt="Github logo" width="150" />
        </router-link>
        <div>
          <a href="https://api.github.com/users" target="_blank" class="navbar-link">API Link</a>
        </div>
      </div>
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

.navbar-link {
  text-decoration: none;
  color: #212529;
  transition: all 0.25s;
  padding: 8px 20px;
  margin-left: 0.5rem;

  &:hover {
    color: #42b983;
  }
}
</style>
