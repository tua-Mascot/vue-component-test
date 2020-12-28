<template>
  <div id="app">
    <conditionsHeader />
  </div>
</template>

<script>
import conditionsHeader from './components/conditions/conditionsHeader.vue';

export default {
  name: 'app',
  components: {
    conditionsHeader,
  },
};
</script>

<style lang='scss'>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 12px;
    text-align: left;
    background-color: #f5f5f7;
    color: #000000;
  }

  #app {
    width: 100%;
    max-width: 960px;
    display: flex;
    justify-content: flex-start;
    flex-wrap: wrap;
  }
</style>
