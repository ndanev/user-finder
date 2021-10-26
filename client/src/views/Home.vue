<template>
  <div class="home">
    <div class="container">
      <div class="row mb-5">
        <div class="col-md-12">
          <form @submit.prevent="findUser">
            <div class="form-group">
              <input
                type="text"
                v-model="searchUser"
                placeholder="Search by username"
                class="form-control"
              />
            </div>
            <button type="submit">
              <i class="fas fa-search"></i> Search
            </button>
          </form>
        </div>
      </div>
      <div v-if="data" class="row">
        <div v-for="user in data" :key="user.id" class="col-12 col-sm-6 col-md-3">
          <router-link :to="`/user/${user.login}`" class="user-card-link">
            <UserCard :image="user.avatar_url" :name="user.login" />
          </router-link>
        </div>
      </div>
      <div v-if="searchData" class="row">
        <div class="col-md-3">
          <router-link :to="`/user/${searchData.login}`" class="user-card-link">
            <UserCard :image="searchData.avatar_url" :name="searchData.login" />
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
      data: null,
      searchUser: '',
      searchData: null,
      loading: false,
      message: ''
    }
  },
  methods: {
    async findUser() {
      const inputData = this.searchUser
      try {
        this.loading = true
        const res = await axios.get('https://api.github.com/users/' + inputData)
        this.searchData = res.data
        this.data = null
        this.loading = false
      } catch (error) {
        console.log(error)
      }
      console.log(this.searchData)
    }
  },
  async created() {
    const url = 'https://api.github.com/users'
    try {
      this.loading = true
      const res = await axios.get(url)
      this.data = res.data
      this.loading = false
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

.home {
  form {
    display: flex;

    input.form-control {
      border-radius: 0;
    }

    div.form-group {
      flex: 3;
    }

    button {
      flex: 1;
      border: 0;
      background-color: #42b983;
      color: #fff;
      transition: all 0.25s;

      &:hover {
        color: #212529;
      }
    }
  }
}

.user-card-link {
  text-decoration: none;
}
</style>
