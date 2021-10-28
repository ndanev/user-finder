<template>
  <div class="user">
    <div class="container">
      <div class="row mb-3 mb-md-5">
        <div class="col-md-12">
          <router-link to="/" class="back">
            <i class="fas fa-long-arrow-alt-left"></i> Back to home
          </router-link>
        </div>
      </div>
      <div v-if="loading" class="row">
        <div class="col-md-12 text-center">
          <img src="@/assets/spinner.gif" alt="Spinner" class="spinner" />
        </div>
      </div>
      <div v-if="user" class="row user-info mb-5">
        <div class="col-md-3 mb-5 mb-md-0 user-info-left">
          <img :src="user.avatar_url" class="img-fluid mb-3" alt />
          <div class="user-name mb-3">{{ user.login }} - {{ user.name }}</div>
          <div v-if="user.location" class="mb-3">
            <i class="fas fa-map-marker-alt"></i>
            {{ user.location }}
          </div>
          <div
            v-if="user.created_at"
            class="mb-4"
          >Member Since: {{ new Date(user.created_at).toLocaleDateString() }}</div>
          <a :href="user.html_url" target="_blank" class="user-button">
            View Profile
            <i class="fas fa-external-link-alt"></i>
          </a>
        </div>
        <div class="col-md-9 user-info-right">
          <div class="mb-3">
            <span class="budge">Repos: {{ user.public_repos }}</span>
            <span class="budge">Gists: {{ user.public_gists }}</span>
            <span class="budge">Followers: {{ user.followers }}</span>
            <span class="budge">Following: {{ user.following }}</span>
          </div>
          <div v-if="user.email" class="mb-3">
            <i class="far fa-envelope"></i>
            {{ user.email }}
          </div>
          <div v-if="user.company" class="mb-3">Company: {{ user.company }}</div>
          <div v-if="user.blog" class="mb-3">
            Blog:
            <a :href="user.blog" target="_blank">{{ user.blog }}</a>
          </div>
          <div v-if="user.bio" class="mb-3">
            Bio:
            <div>{{user.bio}}</div>
          </div>
        </div>
      </div>
      <div v-if="repos" class="row user-repos">
        <h3 class="mb-3">Repositories by {{ user.login }}</h3>
        <div class="row">
          <div class="col-md-12">
            <div class="table-responsive">
              <table class="table">
                <thead>
                  <tr>
                    <th scope="col">id</th>
                    <th scope="col">Created At</th>
                    <th scope="col">Name</th>
                    <th scope="col">Forks</th>
                    <th scope="col">Watchers</th>
                    <th scope="col">Size</th>
                    <th scope="col">Repo Link</th>
                  </tr>
                </thead>
                <tbody v-for="(repo, index) in repos" :key="index">
                  <tr>
                    <td>{{ repo.id }}</td>
                    <td>{{ new Date(repo.created_at).toLocaleDateString() }}</td>
                    <td>{{ repo.name }}</td>
                    <td>{{ repo.forks }}</td>
                    <td>{{ repo.watchers }}</td>
                    <td>{{ repo.size }}</td>
                    <td>
                      <a :href="repo.html_url" target="_blank" class="text-center">
                        <i class="fas fa-external-link-alt"></i>
                      </a>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "User",
  data() {
    return {
      user: null,
      repos: null,
      loading: false
    }
  },
  async created() {
    const username = this.$route.params.username
    try {
      this.loading = true
      const res = await axios.get('https://api.github.com/users/' + username)
      const repos = await axios.get(`https://api.github.com/users/${username}/repos`)
      this.user = res.data
      this.repos = repos.data
      this.loading = false
    } catch (error) {
      console.log(error)
    }
  }
};
</script>

<style lang="scss">
.user {
  padding-top: calc(85px + 60px);
  padding-bottom: 3rem;

  img {
    width: 100%;
  }
  @media (max-width: 767px) {
    padding-top: calc(85px + 20px);
  }
}

.budge {
  font-size: 14px;
  font-weight: 500;
  background-color: #eaeaea;
  padding: 5px 10px;
  display: inline-block;
  border-radius: 20px;
  margin: 0 5px 5px 0;
}

.table > :not(:first-child) {
  border-top: 0 !important;
}

.table i {
  color: #42b983;

  &:hover {
    color: #212529;
    transition: all 0.25s;
  }
}

.user-button {
  text-decoration: none;
  border: 0;
  background-color: #42b983;
  padding: 12px 25px;
  color: #fff;
  transition: all 0.25s;

  &:hover {
    color: #212529;
  }
}

.back {
  color: #212529;
  text-decoration: none;
  transition: all 0.25s;
  &:hover {
    color: #42b983;
  }
}
</style>
