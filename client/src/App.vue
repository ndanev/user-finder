<template>
  <div id="app">
    <Header />
    <router-view />
    <Footer />
  </div>
</template>

<script>
import Header from "@/components/Navbar.vue"
import Footer from "@/components/Footer.vue"
export default {
  name: "App",
  components: {
    Header,
    Footer
  }
};
</script>

<style lang="scss">
* {
  font-family: "Lato", sans-serif;
}

ul {
  margin: 0;
  padding: 0;
}

.spinner {
  width: 200px !important;
}
</style>
