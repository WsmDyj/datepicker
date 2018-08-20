<template>
  <div id="app">
    <Datepicker></Datepicker>
    <ScrollDatepice></ScrollDatepice>
  </div>
</template>

<script>
import Datepicker from './components/Datepicker'
import ScrollDatepice from './components/ScrollDatepice'
export default {
  name: 'App',
  components: {
    Datepicker,
    ScrollDatepice
  }
}
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
