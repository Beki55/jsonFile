<template>
  <div
    style="
      height: 100vh;
      justify-content: center;
      align-items: center;
      display: flex;
    "
  >
    <div>
      <img style="width: 150px" src="../assets/b.png" alt="Logo" />
      <h1>Login</h1>
      <div class="login">
        <input type="email" v-model="email" placeholder="Enter email" />
        <input
          type="password"
          v-model="password"
          placeholder="Enter password"
        />
        <button v-on:click="login">Login</button>
        <p>
          <router-link to="/sign-up">Sign up</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        let response = await axios.get(
          `http://localhost:3000/user?email=${this.email}&password=${this.password}`
        );

        if (response.status === 200 && response.data.length > 0) {
          localStorage.setItem("user-info", JSON.stringify(response.data));
          this.$router.push({ name: "Home" });
        } else {
          alert("Invalid email or password");
        }
      } catch (error) {
        console.error("Error during login:", error);
        alert("An error occurred during login. Please try again.");
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
