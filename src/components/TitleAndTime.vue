<template>
    <div class="title">
        <h2>{{text}}</h2>
        <div>
            {{ timestemp }}
        </div>
    </div>
</template>

<script>
import moment from 'moment'

    export default {
        name: 'TitleAndTime',
        props: ['text', 'dataDate'],
        computed : {
            timestemp: function() {
                return moment(this.dataDate).format('LLLL')
            }
        }
    }
</script>

<style>
.title{
    padding: 2px;
    margin: 9px;
}
</style>