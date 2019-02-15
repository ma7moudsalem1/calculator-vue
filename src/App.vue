<template>
  <div id="app">
    <Copyright msg="Enjoy Vue Calculator" />
    <Calculator />
    <a href="https://github.com/ma7moudsalem1/calculator-vue" target="_blank">Visit Github Repository</a>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import Copyright from './components/Copyright.vue'

export default {
  name: 'app',
  components: {
    Calculator,
    Copyright
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
