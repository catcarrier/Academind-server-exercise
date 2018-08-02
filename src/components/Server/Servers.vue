<template>
    <div class="col-xs-12 col-sm-6">
        <ul class="list-group">
            <app-server v-for="server in servers" :id="server.id" :name="server.name" :status="server.status"></app-server>
        </ul>
    </div>
</template>

<script>
import Server from "./Server.vue";
import { eventBus } from "../../main";

export default {
  data: function() {
    return {
      servers: [
        { id: 0, name: "Seneca", status: "Normal" },
        { id: 1, name: "Onondaga", status: "Normal" },
        { id: 2, name: "Keuka", status: "Offline" },
        { id: 3, name: "Mohawk", status: "Normal" },
        { id: 4, name: "Cayuga", status: "Normal" }
      ]
    };
  },
  components: {
    "app-server": Server
  },
  created() {
    eventBus.$on("serverStatusChange", data => {
      var server = this.servers.find(elem => {
        return elem.id == data.id;
      });
      if(server) {
          server.status=data.status;
      } else {
          console.log("Received serverStatusChange event but could not find matching server! Event was " + data);
      }

    });
  }
};
</script>
    
<style>

</style>
