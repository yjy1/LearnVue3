<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{person.name}}</h2>
  <h2>年龄：{{ person.age }}</h2>
  <h3>工作种类：{{ person.job.type }}</h3>
  <h3>薪水：{{ person.job.salary }}</h3>
  <h3>c:{{ person.job.a.b.c }}</h3>
  <h3>爱好：{{ person.hobies }}</h3>
  <button @click="changeInfo">修改人的信息</button>

</template>

<script>
import {ref,reactive} from 'vue'
export default {
  name: 'App',
  setup(){
    // 数据
    let name =  ref('张三')  
    let age = ref(18)
    let job1 = ref({
      type:'前端工程师',
      salary:'30k'
    })
    /* 
        reactive(target: object): object
    */
    let job = reactive({
      type:'前端工程师',
      salary:'30k',
      a:{
        b:{
          c:333
        }
      }
    })
    // let hobies = ['抽烟','喝酒','烫头']
    let hobies = reactive(['抽烟','喝酒','烫头'])
    
    let person =reactive({
      name: '张三',
      age: 18,
      job: {
        type: '前端工程师',
        salary: '30k',
        a: {
          b: {
            c: 333
          }
        }
      },
      hobies: ['抽烟', '喝酒', '烫头']
    }) 
    // 方法
    function changeInfo(){
      // ref定义的这样修改
      job1.value.type = 'Web前端'
      job1.value.salary = '36k'
      // reactive定义的这样修改
      person.job.type = 'Web前端'
      person.job.salary = '36k'
      person.job.a.b.c = 555
      person.hobies[0] = '学习'
      // console.log(job.a)
      // console.log(hobies[0])
      // console.log(job1.value.type)
      // console.log(person)
      console.log(person.name)
      console.log(person.age)
      console.log(person.job.type)
    }
    
    // 返回一个对象（常用）
    return {
      // name,
      // age,
      // job,
      // hobies,
      person,
      changeInfo
    }
  }
}
</script>
 
