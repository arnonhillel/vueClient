<template>
  <div class="base-demo" style="width: 400px">
    <vue-table-dynamic :params="params"></vue-table-dynamic>
  </div>
  
</template>

<script>
import VueTableDynamic from "vue-table-dynamic";

export default {
  name: "Demo",
  data() {
    return {
      params: {
        data: [
          ["name", "role", "workplace"],
          ["", "", ""],
          ["", "", ""],["", "", ""],
          ["", "", ""],["", "", ""],
          ["", "", ""]
        ],
        header: "row",
        border: true
      }
    };
  },
  components: { VueTableDynamic }
};
</script>


<style lang="scss" scoped>
$angle: 30deg;
.base-demo {
  position: relative;
  display: inline-block;
  vertical-align: middle;
  border: 1px solid;
  text-align: center;
  margin-top: 5px;
  font-size: 14px;
}
</style>

