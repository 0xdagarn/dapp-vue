<template>
  <div id="app">
    <Package />
    <Seaport />
  </div>
</template>

<script>
import Package from './components/Package.vue'
import Seaport from './components/Seaport.vue'

export default {
  name: 'App',
  components: {
    Package,
    Seaport
  }
}
</script>

<style>
</style>
