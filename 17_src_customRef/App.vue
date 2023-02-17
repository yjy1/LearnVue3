<template>
<input type="text" v-model="keyWord">
<h3>{{ keyWord }}</h3>
</template>

<script>
import { ref, customRef } from 'vue'
export default {
  name: 'App',
  setup() {
    // 自定义一个ref--名为myRef
    function myRef(value,delay) {
      let timer
      return customRef((track,trigger) => {
        console.log(track,trigger)
        return {
          get(){
            console.log('有人从myRef这个容器中读取数据了，我把xx给他了')
            track() // 通知vue追踪value的变化（提前和get商量一下，让他认为这个value是有用的）
            return value
          },
          set(newValue){
            console.log(`有人把myRef这个容器的数据改为了：${value}`)
            clearTimeout(timer)
            timer = setTimeout(() => {
              value  = newValue
              trigger() // 通知vue去重新解析模板
            }, delay);
          }
        }
      })
    }
    // let keyWord = ref('hello') //使用vue提供的ref
    let keyWord = myRef('hello',500) //使用自定义的ref

    return {
      keyWord
    }
  }
}
</script>
 
