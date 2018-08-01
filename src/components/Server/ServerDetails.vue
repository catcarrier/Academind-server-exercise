<template>
    <div class="col-xs-12 col-sm-6">
        <p>id: {{ id }} Name: {{ name }} status: {{ status }} <button @click="toggleStatus">toggle</button></p>
    </div>

</template>

<script>
import { eventBus } from '../../main';
export default {
    props: ['id','name','status'],
    data: function(){
        return {}
    },
    methods: {
        toggleStatus() {
            // status switches between Normal and Offline
            this.status = this.status == 'Normal' ? 'Offline' : 'Normal';
            eventBus.$emit('serverStatusChange', {id: this.id, status: this.status});
        }
    },
    created() {
        eventBus.$on('showServerDetails', (data) => {
            this.id = data.id;
            this.name = data.name;
            this.status=data.status;
        })
    }
}
</script>

<style>

</style>
