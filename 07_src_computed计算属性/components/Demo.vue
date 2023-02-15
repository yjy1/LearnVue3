<template>
    <h1>一个人的信息</h1>
    姓：<input type="text" v-model="person.firstName">
    <br> 
    名：<input type="text" v-model="person.lastName"> 
    <br> 
    全名：<span>{{ person.fullName }}</span>
    <br> 
    全名：<input type="text" v-model="person.fullName"> 

</template>

<script>
import { def } from '@vue/shared'
import { ref, reactive,computed } from 'vue'
export default {
    name: 'Demo',
    // vue2写法
    /* computed:{
        fullName(){
          return  this.person.firstName + this.person.lastName
        }
    }, */
    setup() {
        let person = reactive({
            firstName: '张',
            lastName:'三'
        })
        // 计算属性一简写(没有考虑计算属性被修改的情况)
        /* person.fullName = computed(()=>{
            return person.firstName + person.lastName
        }) */
        // 计算属性一完整写法(考虑读和写)
        person.fullName = computed( {
            get(){
                return person.firstName + '-' + person.lastName
            },
            set(value){
                person.firstName = value.split('-')[0]
                person.lastName = value.split('-')[1]
            }
        })
        // 返回一个对象（常用）
        return {
            person,
        }
    }
}
</script>
 
