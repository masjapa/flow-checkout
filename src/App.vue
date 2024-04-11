<template>
  <div id="app">
    <CheckoutForm />
  </div>
</template>

<script>
import CheckoutForm from '@/components/CheckoutForm.vue'

export default {
  name: 'App',
  components: {
    CheckoutForm
  }
}
</script>

<style>
body {
  padding: 0 !important;
  margin: 0 !important;
  background-color: #FFFAE6;
}
#app {
  font-family: interUi, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
