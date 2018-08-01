<template>
    <li class="list-group-item server" :class="{selected:isSelected}" @click="showServer">
        <span>{{ name }} </span>
        <span :class="{normal: isNormal, offline: !isNormal }">[{{ status }}]</span>
    </li>
</template>

<script>
import { eventBus } from "../../main";

export default {
    props: ['id','name','status'],
    data: function() {
        return { selected: false }
    },
    computed: {
        isNormal: function(){ return this.status=='Normal' },
        isSelected: function(){ return this.selected }
    },
    methods: {
        showServer() {
            eventBus.$emit('showServerDetails', { id: this.id, name: this.name, status: this.status });
        }
    },
    created() {
        eventBus.$on('showServerDetails', (data) => {
            this.selected = (data.id == this.id);
        })
    }
}
</script>

<style>
.normal {
   color: green; 
}
.offline {
    color: red
}
.server {
    cursor: pointer;
}
.selected {
    background-color: lightblue;
}
</style>


