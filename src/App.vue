<template>
<v-header></v-header>
<router-view></router-view>
</template>

<script lang="ts">
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    'v-header': Header
  }
}
</script>
<style lang="scss">
@import './assets/css/theme.scss';
@import './assets/css/common.scss';
@import './assets/fonts/font.scss';
@import '//at.alicdn.com/t/font_2372523_u3if0pm6hhn.css';
#app {
  width: 100%;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

</style>