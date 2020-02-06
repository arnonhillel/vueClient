<template>
  <div>
    <div v-bind:key="user" v-for="user in users">
      <User v-bind:User="user" />
    </div>
  </div>
</template>

<script>
import User from './User.vue';

export default {
  name: "User",
  components: {
    User
  },
  props: ["user"]
}
</script>

<style scoped>

</style>