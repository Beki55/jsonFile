<template>
  <div>
    <Header />
  <div
    style="
      height: 100vh;
      justify-content: center;
      align-items: center;
      display: flex;
    "
  >
    <div>
      <h1 style="margin-bottom: 40px;">Hello user, wellcome to Add page</h1>
      <form action="" class="add">
        <input
          type="text"
          name="name"
          placeholder="Enter name"
          v-model="restuarant.name"
        />
        <input
          type="text"
          name="address"
          placeholder="Enter address"
          v-model="restuarant.address"
        />
        <input
          type="text"
          name="contact"
          placeholder="Enter contact"
          v-model="restuarant.contact"
        />
        <button type="button" v-on:click="addRestuarant">
          Add new restuarant
        </button>
      </form>
    </div>
  </div>
  </div>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "Add",
  components: {
    Header,
  },
  data() {
    return {
      restuarant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
    async addRestuarant() {
      console.warn(this.restuarant);
      const result = await axios.post("http://localhost:3000/resturant", {
        name: this.restuarant.name,
        address: this.restuarant.address,
        contact: this.restuarant.contact,
      });
      if (result.status == 201) {
        this.$router.push({ name: "Home" });
      }
      console.warn("result", result);
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>

<style></style>
