<template>
    <div class="child">
        <h3>我是Child组件（子）</h3>
        <Son />
    </div>
</template>
<script>
import {inject} from 'vue'
import Son from '../components/Son.vue'
export default {
    name: 'Child',
    components: { Son },
    setup(){
        let car = inject('car')
        console.log(car)
        return {car}
    }
}
</script>
<style>
.child {
    background-color: skyblue;
    padding: 10px;
}
</style>