<template>
    <h4>当前求和为: {{ sum }}</h4>
    <button @click="sum++">点我+1</button>
    <hr>
    <h2>姓名：{{ name }}</h2>
    <h2>年龄：{{ age }}</h2>
    <h2>薪资：{{ job.j1.salary }}K</h2>
    <h2 v-show="person.car">座驾信息：{{ person.car }}</h2>
    <button @click="name += '~'">修改姓名</button>
    <button @click="age++">年龄增长</button>
    <button @click="job.j1.salary++">涨薪</button>
    <button @click="showRawPerson">输出最原始的person</button>
    <button @click="addCar">给人添加一台车</button>
    <button @click="person.car.name+='!'">换车名</button>
    <button @click="person.car.price++">换价格</button>
    <button @click="changePrice">换价格2</button>
</template>

<script>
import {ref, reactive, toRef ,toRefs,toRaw,markRaw} from 'vue'
export default {
    name: 'Demo',
    setup() {
        let sum = ref(0)
        let person = reactive({
            name: '张三',
            age: 18,
            job: {
                j1: {
                    salary: 20
                }
            }
        }) 
        function showRawPerson(){
            // let p = toRaw(person)
            // p.age++
            // console.log(p)
            
            sum = toRaw(sum)
            console.log(sum)
        }
        function addCar(){
            let car = {name:'奔驰',price:'40'}
            person.car = markRaw(car)
        }
        function changePrice(){
            person.car.price++
            console.log(person.car.price)
        }
        return{
            person,
            ...toRefs(person),
            sum,
            showRawPerson,
            addCar,
            changePrice
        }
    }
}
</script>
 
