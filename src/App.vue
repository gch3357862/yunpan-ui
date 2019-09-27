<template>
  <div id="app">
    <img src="./assets/logo.png" alt="png">
    <router-view style="margin-top:100px;"></router-view>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-size: medium;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
}
</style>
