<script>

export default {
  name: "App",
};
</script>

<template>
  <div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  padding: 0;
  margin: 0;
}
.register input,
.login input,
.add input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid lightcoral;
}
.register button,
.login button,
.add button {
  width: 320px;
  height: 40px;
  border: 1px solid lightcoral;
  background: lightcoral;
  color: #fff;
  cursor: pointer;
}
</style>
