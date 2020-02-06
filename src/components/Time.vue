<template>
  <div>
    <form @submit.prevent="setTime">
      <input type="time" v-model="time" name="time" placeholder="Add users..." />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
export default {
  name: "Time",
  data() {
    return {
      time: ""
    };
  },
  methods: {
    setTime() {
      const nawTime = {
        time: this.time
      };
      this.$emit("set-time", nawTime);
      this.time = "";
    }
  }
};
</script>

<style scoped>
form {
  display: grid, flex;
}

input[type="text"] {
  flex: 10;
  padding: 5px;
  margin-bottom: 5px;
}

input[type="submit"] {
  flex: 2;
}
</style>