<template>
  <div class="home">
    <div class="container">
      <div class="row justify-content-center mb-5">
        <div class="col-md-6 text-center mb-3 mb-md-5">
          <h2>Explore github users and their repositories information using our service</h2>
        </div>
        <div class="col-md-12">
          <form @submit.prevent="findUser">
            <div class="form-group">
              <input
                type="text"
                v-model="searchUser"
                placeholder="Search by username"
                class="form-control"
                required
              />
            </div>
            <button type="submit">
              <i class="fas fa-search"></i> Search
            </button>
          </form>
        </div>
      </div>
      <div v-if="loading" class="row mb-5">
        <div class="col-md-12 text-center">
          <img src="@/assets/spinner.gif" alt="Spinner" class="spinner" />
        </div>
      </div>
      <div v-if="message" class="row mb-5">
        <div class="col-md-12 text-center">
          <div class="error-message">{{message}}</div>
        </div>
      </div>
      <div v-if="data" class="row">
        <div v-for="user in data" :key="user.id" class="col-6 col-sm-6 col-md-3">
          <router-link :to="`/user/${user.login}`" class="user-card-link">
            <UserCard :image="user.avatar_url" :name="user.login" />
          </router-link>
        </div>
      </div>
      <div v-if="searchData" class="row">
        <div class="col-md-12">
          <div class="text-center mb-3">
            <button @click="getUsers()" class="reset">Show all users</button>
          </div>
        </div>
        <div class="col-6 col-sm-6 col-md-3">
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
      searchUser: null,
      searchData: null,
      loading: false,
      message: null
    }
  },
  methods: {
    async findUser() {
      const inputData = this.searchUser
      this.searchUser = null
      try {
        this.loading = true
        const res = await axios.get('https://api.github.com/users/' + inputData)
        this.searchData = res.data
        this.data = null
        this.loading = false
        this.searchUser = null
        this.message = null
      } catch (error) {
        this.message = 'Not user found!'
        this.loading = false
        console.log(error)
      }
    },
    async getUsers() {
      try {
        this.loading = true
        const res = await axios.get('https://api.github.com/users')
        this.data = res.data
        this.searchData = null
        this.message = null
        this.loading = false
      } catch (error) {
        this.message = 'Not user found!'
        console.log(error)
        this.loading = false
      }
    }
  },
  created() {
    this.getUsers()
  }
}
</script>

<style lang="scss">
.home {
  padding-top: calc(85px + 60px);

  @media (max-width: 767px) {
    padding-top: calc(85px + 20px);
  }
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

.reset {
  background-color: #42b983;
  border: 0;
  color: #fff;
  padding: 5px 10px;
}

.error-message {
  color: #e55353;
}
</style>
