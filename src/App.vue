<template>
  <div id="app">
    <store-main-wrapper></store-main-wrapper>
  </div>
</template>

<script>
import storeMainWrapper from './components/store-main-wrapper';

export default {
  name: 'app',
  components: {
    storeMainWrapper
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 20px;
}
</style>
