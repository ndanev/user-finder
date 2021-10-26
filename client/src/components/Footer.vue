<template>
  <footer class="footer">
    <div class="container">
      <div class="row">
        <div class="col-md-6 d-flex align-items-center">
          <div class="copyrights mb-3 mb-md-0 mx-auto mx-md-0 text-center text-md-left">
            &copy; {{ new Date().getFullYear() }}, powerd by
            <span>Nemanja Danev</span>
          </div>
        </div>
        <div class="col-md-6 d-flex justify-content-center justify-content-md-end">
          <a href="https://github.com/ndanev?tab=repositories" target="_blank">
            <i class="fab fa-github-square" />
          </a>
          <a href="https://www.linkedin.com/in/nemanjadanev/" target="_blank">
            <i class="fab fa-linkedin" />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style lang="scss">
.footer {
  padding: 16px 0;
  border-top: 1px solid #d9d9d9;
}

.copyrights {
  span {
    color: #42b983;
  }
}

.footer i {
  color: #212529;
  font-size: 1.6rem;
  margin-left: 0.5rem;
  transition: all 0.5s;

  &:hover {
    color: #42b983;
  }
}
</style>
