<template>
  <div id="app">
    <Alert/>
    <VueClock />
    <router-view />
    <Time v-on:set-time="setTime" />
    <!-- <Table/> -->

    <table class="table table-striped" align="center">
      <tbody>
        <th scope="row">name</th>
        <th scope="row">role</th>
        <th scope="row">workplace</th>
        <tr v-for="(user,i) in users" :key="i">
          <td scope="row">{{ user.name }}</td>
          <td scope="row">{{ user.role }}</td>
          <td scope="row">{{ user.workplace }}</td>
        </tr>
      </tbody>
    </table>

    <users v-on:user="users" />
  </div>
</template>

<script>
import VueClock from "./components/VueClock";
// import Table from "./components/Table.vue";
import Users from "./components/Users";
import Alert from "./components/Alert";
import Time from "./components/Time";
import axios from "axios";
// import VueMoment from 'vue-moment'
// import  Store  from 'vuex';

export default {
  name: "app",
  components: {
    VueClock,
    Alert,
    // Table,
    Time,
    Users
  },
  data() {
    return {
      users: []
    };
  },
  methods: {
    async setTime(newTime) {
      localStorage.setItem("data", {});
      const today = new Date().toLocaleString();
      const time = newTime.time.toString();
      var currentTime = this.parseTime(today);
      var hh = parseInt(time.substring(0, 2));
      var mm = parseInt(time.substring(3, 5));
      var ss = 11;
      var requestTime = { hh: hh, mm: mm, ss: ss };
      var timeout =0
      if(!isNaN(requestTime.hh)){
       timeout = this.getMyTimout(requestTime, currentTime);
      }    
      setTimeout(function() {
        axios
          .get("http://localhost:8081/execute")
          .then(
            response => (
              (this.users = response.data),
              localStorage.setItem("data", JSON.stringify(response.data), location.reload())
            )
          )
          .catch(err => console.log(err));
      }, timeout);
      this.$forceUpdate();
    },
    parseTime(s) {
      var part = s.match(/(\d+):(\d+)(?: )?(am|pm)?/i);
      var hh = parseInt(part[1], 10);
      var mm = parseInt(part[2], 10);
      var ap = part[3] ? part[3].toUpperCase() : null;
      if (ap === "AM") {
        if (hh == 12) {
          hh = 0;
        }
      }
      if (ap === "PM") {
        if (hh != 12) {
          hh += 12;
        }
      }
      return { hh: hh, mm: mm, ss: 11 };
    },
    getMyTimout(requestTime, currentTime) {
      var carTime =
        +currentTime.hh + ":" + currentTime.mm + ":" + currentTime.ss;
      var reqTime =
        +requestTime.hh + ":" + requestTime.mm + ":" + requestTime.ss;
      // curTimeMil = (currentTime.hh*60*60 +currentTime.mm*60)*1000
      const moment = require("moment");
      var a = moment(carTime, "HH:mm:ss").diff(moment(reqTime, "HH:mm:ss"));
      var b = moment(reqTime, "HH:mm:ss").diff(moment(carTime, "HH:mm:ss"));
      var c = this.max(a,b)
      return parseInt(c);
    },
    max(a,b){
      if(a>b){
      return a 
      }else{return b}

    }
  },

  created() {
    this.users = JSON.parse(localStorage.getItem("data"));
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
td,
th {
  border: 1px solid black;
  min-width: 300px;
}
table {
  align-self: center;
}
</style>
