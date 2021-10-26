<template>
  <div class="home">
    <div class="container">
      <div class="row">
        <div v-for="user in data" :key="user.id" class="col-12 col-sm-6 col-md-3">
          <router-link :to="`/user/${user.login}`" class="user-card-link">
            <UserCard :image="user.avatar_url" :name="user.login" />
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserCard from '@/components/UserCard'
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    UserCard
  },
  data() {
    return {
      data: null
    }
  },
  async created() {
    const url = 'https://api.github.com/users'
    try {
      const res = await axios.get(url)
      this.data = res.data
      console.log(this.data)
    } catch (error) {
      console.log(error)
    }
  }
}
</script>

<style lang="scss">
.home {
  padding-top: calc(85px + 60px);
}

.user-card-link {
  text-decoration: none;
}
</style>
