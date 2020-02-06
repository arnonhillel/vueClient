<template>
  <div class="user" v-bind:class="{'user.name':user.name}">
    <p>{{users.name}} {{users.role}} {{users.workspace}}</p>
  </div>
</template>

<script>
export default {
  name: "User",
  props: ["user"]
};
</script>

<style scoped>
.user {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
</style>
