<template>
  <div class="app">
    <h3>我是APP组件 </h3>
    <Suspense>
      <template v-slot:default>
        <Child/>
      </template>
      <template v-slot:fallback>
        <h2>加载中...</h2>
      </template>
    </Suspense>
</div>
</template>
<script>
// import Child from './components/Child' //静态引入
import { defineAsyncComponent } from 'vue';
const Child = defineAsyncComponent(()=>import('./components/Child.vue') ) //异步引入
export default {
  name: 'App',
  components: { Child },
}
</script>
<style>
.app {
  background-color: gray;
  padding: 10px;
}
</style>