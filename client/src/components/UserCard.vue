<template>
  <article class="user-card">
    <img :src="image" alt />
    <div class="user-card-name">{{ name }}</div>
  </article>
</template>

<script>
export default {
  name: "UserCard",
  props: {
    name: {
      type: String,
      required: true
    },
    image: {
      type: String,
      required: true
    }
  }
};
</script>

<style lang="scss">
.user-card {
  transition: all 0.25s ease-in-out;
  border: 1px solid #d9d9d9;
  margin-bottom: 3rem;
  transition: all 0.25s;

  &:hover {
    transform: scale(1.02);
  }

  img {
    width: 100%;
  }

  .user-card-name {
    color: #24292f;
    font-size: 1.2rem;
    padding: 1rem;
    text-align: center;

    @media (max-width: 991px) {
      font-size: 1rem;
      padding: 0.5rem;
    }
  }
}
</style>
