<template>
  <div id="app">
    <calendar></calendar>
  </div>
</template>

<script>
  import Calendar from '@/components/Calendar'

  export default {
    name: 'clock',
    components: {
      Calendar
    }
  }
</script>

<style>
  /* CSS */
#app {
  -webkit-app-region: drag;
  height: 100vh;
  width: 100vw;
  box-sizing: border-box;
  padding: 10px;
  overflow: hidden;
}
</style>
