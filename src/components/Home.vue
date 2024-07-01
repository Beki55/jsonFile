<template>
  <div>
    <Header />
    <h1 style="margin: 40px">Hello {{ name }} , wellcome to home page</h1>
    
    <section id="education">
      <div class="education">
        <div class="edu-title">
          <h1>Try lorem</h1>
          <span>———o———</span>
      </div>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Aut ex perspiciatis cumque similique, illum veritatis? Natus veritatis iure atque dolor in eius, qui consequuntur veniam, voluptate quibusdam, quis voluptates nulla!

      </div>
    </section>

    <p style="margin: 60px;">Restuarant info which are available in this system</p>

    <div style="display: flex; justify-content: center; margin: 10px;">
      <table border="1">
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Contact</th>
          <th>Address</th>
          <th>Actions</th>
        </tr>
        <tr v-for="item in restuarant" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.contact }}</td>
          <td>{{ item.address }}</td>
          <td>
            <router-link :to="'/update/' + item.id">Update</router-link>
            <button class="btn" v-on:click="deleteRestuarant(item.id)">
              Delete
            </button>
          </td>
        </tr>
      </table>
    </div>
    <p style="margin: 60px;">Users info who are capable of login in to this system</p>
    <div style="display: flex; justify-content: center; margin: 10px;">
      <table border="1">
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>email</th>
          <th>password</th>
          <th>Actions</th>
        </tr>
        <tr v-for="item in user" :key="item.id">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.password }}</td>
          <td>
            <router-link :to="'/update/' + item.id">Update</router-link>
            <button class="btn" v-on:click="deleteUser(item.id)">
              Delete
            </button>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      name: "",
      restuarant: [],
      user:[]
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleteRestuarant(id) {
      let result = await axios.delete("http://localhost:3000/resturant/" + id);
      console.warn(result);
      if (result.status == 200) {
        this.loadData();
      }
    },
    async deleteUser(id) {
      let result2 = await axios.delete("http://localhost:3000/user/" + id);
      console.warn(result2);
      if (result2.status == 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;

      if (!user) {
        this.$router.push({ name: "SignUp" });
      }

      let result = await axios.get("http://localhost:3000/resturant");
      console.warn(result);
      this.restuarant = result.data;

      let result2 = await axios.get("http://localhost:3000/user");
      console.warn(result2);
      this.user = result2.data;
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>

<style>
td {
  width: 160px;
  height: 40px;
}
.btn {
  padding: 10px;
  margin: 10px;
  background-color: lightcoral;
  border-radius: 20px;
}
section{
  margin: 50px;
  font-size: larger;
  font-weight: bolder;
  color: blue;
}

</style>
