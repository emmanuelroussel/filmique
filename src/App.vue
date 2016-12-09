<template>
  <div id="app">
    <home></home>
  </div>
</template>

<script>
import Home from './components/Home';

export default {
  name: 'app',
  components: {
    Home,
  },
};
</script>

<style src="assets/css/normalize.css"></style>
<style src="assets/css/skeleton.css"></style>

<style>
#app {
  text-align: center;
  margin-top: 150px;
}
</style>
