<template>
  <div id="app">
    <VueClock/>
    <AddValue v-on:add-value="addValue" />
    <Table/>
  </div>
</template>

<script>
import VueClock from './components/VueClock.vue';
import Table from './components/Table.vue';
import AddValue from './components/addValue.vue';

export default {
  name: 'app',
  components: {
    VueClock,
    Table,
    AddValue
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
