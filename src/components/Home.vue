<template>
  <div class="container home">
    <div class="row">
      <h1 class="logo logo-full-size">filmique</h1>
      <h4>Enter a theme. Find movies.</h4>
      <input v-model="input" v-on:keyup.enter="search" class="input-home" type="text" placeholder="Ex: Space, World War 2, Gangster, etc." />
      <button v-on:click="search" class="button-primary">Find films</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      input: ''
    }
  },
  methods: {
    search: function () {
      this.$emit('search', this.input)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
}
.logo {
  color: #F2545B;
  font-weight: normal;
}
.logo-full-size {
  font-size: 3.3em;
}
/* Larger than phablet */
@media (min-width: 550px) {
  .logo-full-size {
    font-size: 4em;
  }
}
.input-home {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  max-width: 550px;
}
</style>
