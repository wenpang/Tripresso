<template>
  <div id="app" style="background-color: linen">
    <index/>
  </div>
</template>

<script>
import index from '../src/components/index'

export default {
  name: 'app',
  components: {
    index
  }
}
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  overflow: hidden;
}
</style>
