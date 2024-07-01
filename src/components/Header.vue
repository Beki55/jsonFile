<template>
  <div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add restuarant</router-link>
    <a v-on:click="logout" href="">Log out</a>
    <p style="display: flex; justify-content: end;">
      <router-link to="/login">Login</router-link>
      <router-link to="/sign-up">Sign Up</router-link>
    </p>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "SignUp" });
    },
  },
};
</script>

<style>
.nav {
  background-color: #333;
  overflow: hidden;
  padding: 0 20px;
}
.nav a {
  float: left;
  color: #f2f2f2f2;
  padding: 14px 16px;
  text-align: center;
  font-size: 17px;
  text-decoration: none;
  margin-right: 5px;
}
.nav a:hover {
  background-color: #ddd;
  color: #333;
}
</style>
