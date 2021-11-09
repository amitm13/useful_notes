<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" class="mx-auto">
    <Countdown
      :year='2021'
      :month='11'
      :date='22'
      :hour='0'
      :minute='0'
      :seconds='0'
    />
  </div>
</template>

<script>
import Countdown from './components/Countdown.vue'

export default {
  name: 'App',
  components: {
    Countdown
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
