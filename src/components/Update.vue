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
      class="home"
    >
      <div>
        <h1 style="margin-bottom: 60px;">Hello user, wellcome to Update page</h1>
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
          <button type="button" v-on:click="updateRestuarant">
            Update restuarant
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
  name: "Update",
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
    async updateRestuarant() {
      console.warn();
      const result = await axios.put(
        "http://localhost:3000/resturant/" + this.$route.params.id,
        {
          name: this.restuarant.name,
          address: this.restuarant.address,
          contact: this.restuarant.contact,
        }
      );
      if (result.status == 200) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }

    const result = await axios.get(
      "http://localhost:3000/resturant/" + this.$route.params.id
    );
    // console.warn(this.$route.params.id)
    console.warn(result.data);
    this.restuarant = result.data;
  },
};
</script>

<style>
.home {
  /* margin: 0 auto; */
}
</style>
