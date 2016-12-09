<template>
  <div class="home">
    <h1 class="logo logo-full-size">filmique</h1>
    <h4>Search for any theme and get a list of films corresponding to that theme</h4>
    <input class="input-home" type="text" placeholder="Ex: Space, World War 2, Gangster, etc." />
    <button class="button-primary">Find films</button>
  </div>
</template>

<script>
export default {
  name: 'home',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.logo {
  color: #F2545B;
  font-weight: normal;
  font-size: 4em;
}
.input-home {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 600px;
}
</style>
