<template>
<router-view></router-view>
</template>

<script lang="ts">
export default {
  name: 'App'
}
</script>
<style lang="scss">
body {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  font-weight: 400;
  color: #757575;
  background-color: #f8fafc;
}
#app {
  width: 100%;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
</style>
