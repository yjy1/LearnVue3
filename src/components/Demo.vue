<template>
    <h4>当前的x值是: {{ x.y }}</h4>
    <button @click="x.y++">点我x+1</button>
    <hr>
    <h4>{{ person }}</h4>
    <h2>姓名：{{ name }}</h2>
    <h2>年龄：{{ age }}</h2>
    <h2>薪资：{{ job.j1.salary }}K</h2>
    <button @click="name += '~'">修改姓名</button>
    <button @click="age++">年龄增长</button>
<button @click="job.j1.salary++">涨薪</button>
</template>

<script>
import {ref, reactive, toRef ,toRefs,shallowReactive,shallowRef} from 'vue'
export default {
    name: 'Demo',
    setup() {
        // let person = shallowReactive({ // 只考虑对象类型的第一层
        let person = reactive({
            name: '张三',
            age: 18,
            job: {
                j1: {
                    salary: 20
                }
            }
        }) 
        let x = shallowRef({
            y:0
        })
        console.log('%%%%%%%',x)
        return{
            person,
            ...toRefs(person),
            x
        }
    }
}
</script>
 
