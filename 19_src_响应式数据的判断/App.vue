<template>
  <div class="app">
    <h3>我是APP组件 </h3>
</div>
</template>
<script>
import { ref,reactive,toRefs,readonly ,isRef,isReactive,isProxy,isReadonly,  } from 'vue';
export default {
  name: 'App',
  setup(){
    let car = reactive({
      name:'奔驰',
      price:'40w'
    })
    let sum = ref(0)
    let car2 = readonly(car)

    console.log(isRef(sum))
    console.log(isReactive(car))
    console.log(isReadonly(car2))
    console.log(isProxy(car))
    console.log(isProxy(car2))
    return { ...toRefs(car) }
  }
}
</script>
<style>
.app {
  background-color: gray;
  padding: 10px;
}
</style>