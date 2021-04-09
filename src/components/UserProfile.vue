<template>
  <div class="app">
    {{ fullName }} - @{{ user.username }}
    <button v-on:click="followUser">Follow</button>
  </div>
  <div class="app"><strong>Followers: </strong> {{ followers }}</div>
  <div class="app" v-if="user.isAdmin">ADMIN</div>
  <div class="app" v-else>pleb</div>

  <div class="app" v-for="twoot in user.twoots" :key="twoot.id">
    <!-- mapping -->
    {{ twoot.content }}
  </div>
</template>

<script>
export default {
  name: "UserProfile",
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "mafaro___",
        firstName: "mafaro",
        lastName: "Vue",
        email: "mafaro@email.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "first twoot" },
          { id: 2, content: "learning vue for the first time" },
        ],
      },
    };
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(this.user.username, "has a new follower");
      }
    },
  },

  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },

  methods: {
    followUser() {
      this.followers++;
    },
  },

  mounted() {
    this.followUser();
  },
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  align-items: center;
  display: flex;
  flex-direction: column;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  width: 25%;
}
</style>
