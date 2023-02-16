<template>
    <h4>{{ person }}</h4>
    <h2>姓名：{{ name }}</h2>
    <h2>年龄：{{ age }}</h2>
    <h2>薪资：{{ job.j1.salary }}K</h2>
    <button @click="name += '~'">修改姓名</button>
    <button @click="age++">年龄增长</button>
<button @click="job.j1.salary++">涨薪</button>
</template>

<script>
import {ref, reactive, toRef ,toRefs} from 'vue'
export default {
    name: 'Demo',
    setup() {
        let person = reactive({
            name: '张三',
            age: 18,
            job: {
                j1: {
                    salary: 20
                }
            }
        })
        // let name1 = person.name
        // console.log('%%%', name1)
        // let name2 = toRef(person, 'name')
        // console.log('---', name2)

        const x = toRefs(person)
        console.log('toRefs',x)

        // 返回一个对象（常用）
        /*   return {
             person,
             name:toRef(person,'name'),
             age: toRef(person,'age'),
             salary: toRef(person.job.j1,'salary'),
          } */
       /*  return {
            person,
            name: ref(person.name),
            age: ref(person.age),
            salary: ref(person.job.j1.salary),
        } */
        return{
            ...toRefs(person)
        }
    }
}
</script>
 
