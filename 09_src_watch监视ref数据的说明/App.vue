<template>
  <Demo  >
    <template v-slot:qwe >
      <span>ycj</span>
    </template>
  </Demo>
</template>

<script>
import Demo from './components/Demo.vue'
export default {
  name: 'App',
  components: { Demo },
  setup(){
    function showHelloMsg(value){
      alert(`你好啊,你触发了hello事件,我收到的参数是${value}`)
    }
    return {
      showHelloMsg
    }
  }
}
</script>
 
