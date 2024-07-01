<template>
    <div style="height: 100vh; justify-content: center; align-items: center; display: flex;">
  <div>
    <img style="width: 150px" src="../assets/b.png" alt="" />
    <h1>Sign up</h1>
    <div class="register">
      <input type="text" v-model="name" placeholder="Enter name" />
      <input type="email" v-model="email" placeholder="Enter email" />
      <input type="password" v-model="password" placeholder="Enter password" />
      <button v-on:click="signUp">Sign up</button>
      <p>
        <router-link to="/login">Login</router-link>
      </p>
    </div>
  </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/user", {
        email: this.email,
        name: this.name,
        password: this.password,
      });

      console.warn(result);
      if (result.status == 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted()
  {
    let user = localStorage.getItem("user-info");
    if(user){
        this.$router.push({ name: "Home" });

    }
  }
};
</script>

<style>
.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid lightcoral;
}
.register button {
  width: 320px;
  height: 40px;
  border: 1px solid lightcoral;
  background: lightcoral;
  color: #fff;
  cursor: pointer;
}
</style>
