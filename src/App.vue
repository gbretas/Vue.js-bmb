<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue';
</script>

<template> 
    <div class="container-fluid">
      <HelloWorld/>
    </div>
</template>

<style>
@import '@/assets/base.css';

#app {
  margin: 0 auto;
  font-weight: normal;
}

</style>
