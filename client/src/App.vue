<template>
  <div id="app">
    <Header />
    <router-view />
  </div>
</template>

<script>
import Header from "@/components/Navbar.vue"
export default {
  name: "App",
  components: {
    Header
  }
};
</script>

<style lang="scss">
* {
  font-family: "Lato", sans-serif;
}
</style>
