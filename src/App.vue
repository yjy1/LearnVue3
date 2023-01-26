<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{name}}</h2>
  <h2>年龄：{{ age }}</h2>
  <button @click="changeInfo">修改人的信息</button>

</template>

<script>
import {ref} from 'vue'
export default {
  name: 'App',
  setup(){
    // 数据
    let name =  ref('张三') /* ref(value: string): Ref<string>
 */
    let age = ref(18)
    // 方法
    function changeInfo(){
      // name = '李四'
      // age = 38
      name.value = '李四'
      age.value = 38
      console.log(name,age)
    }
    
    // 返回一个对象（常用）
    return {
      name,
      age,
      changeInfo
    }
  }
}
</script>
 
