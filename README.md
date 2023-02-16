## 1.拉开序幕的setup
    1.理解:Vue3.0中一个新的配置项，值为一个函数
    2.setup是所有Composition API (组合API)“表演的舞台”
    3.组件中所用到的:数据、方法等等，均要配置在setup中。
    4.setup函数的两种返回值:
        1.若返回一个对象，则对象中的属性、方法,在模板中均可以直接使 用。(重点关注!)
        2.若返回一个渲染函数: 则可以自定义染内容。 (了解)
    5.注意点
        1.尽量不要与Vue2x配置混用
            .Vue2.x配置(data、methos、computed...) 中可以访问      到    setup中的属性、方法
            .但在setup中不能访问到Vue2.x配置(data、methos、computed...)
            .如果有重名,setup优先。
        2.setup不能是一个async函数，因为返回值不再是retun的对象,而是promise,模板看不到return对象中的属性


## 2.ref函数
    作用:定义一个响应式的数据
    语法:const xxx = ref(initValue)
        .创建一个包含响应式数据的引用对象 (reference对象,简称ref对象)
        .JS中操作数据:xxx.value
        .模板中读取数据:不需要.value，直接: <div>{{xxx]}</div>
    备注:
        .接收的数据可以是: 基本类型、也可以是对象类型 
        .基本类型的数据:响应式依然是靠object.defineProperty()的get与set 完成的
        .对象类型的数据:内部“求助”了Vue3.0中的一个新函数--reactive函数。 

## 3.reactive函数
    .作用: 定义一个对象类型的响应式数据 (基本类型不要用它，要用 ref 函数)
    .语法: const 代理对象= reactive(源对象)接收一个对象(或组)，返回一个代理对象 ( Proxy的实例对象，简称proxy对象)
    .reactive定义的响应式数据是“深层次的”。
    .内部基于 ES6的 Proxy 实现，通过代理对象操作源对象内部数据进行操作.


## Vue3.0的响应式
    实现原理:
    .通过Proxy (代理): 拦截对象中任意属性的变化,包括: 属性值的读写、属性的添加、性的删除等.
    .通过Reflect (反射):对源对象的属性进行操作。
    .MDN文档中描述的Proxy与Reflect:
        Proxy: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy
        Reflect: https://developer.mozila.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect
            new Proxy(data,{
                // 拦截读取属性值
                get (target, prop) {
                    return Reflect.get(target, prop)
                }
                // 拦截设置属性值或添加新属性
                set (target, prop, value) (
                    return Reflect.set(target, prop, value)
                }
                // 拦截删除属性
                deleteProperty (target,prop) {
                    return Reflect.deleteProperty(target, prop)
                }
            }）
            proxy.name = 'tom'


## 5.reactive对比ref
    .从定义数据角度对比:
        .ref用来定义: 基本类型数据
        .reactive用来定义: 对象 (或数组)类型数据
        .备注: ref也可以用来定义对象(或数组)类型数据它内部会自动通过 reactive 转为代理对象。
    .从原理角度对比:
        .ref通过object.defineProperty()的 get 与 set 来实现响应式(数据劫持)
        .reactive通过使用Proxy来实现响应式(数据劫持)，并通过Reflect操作源对象内部的数据
    .从使用角度对比:
        .ref定义的数据: 操作数据需要 .value，读取数据时模板中直接读取不需要 value
        .reactive定义的数据: 操作数据与读取数据: 均不需要 value。


## 6.setup的两个注意点
    .setup执行的时机
        .在beforeCreate之前执行一次，this是undefined。 
    .setup的参数.
        .props: 值为对象，包含: 组件外部传递过来，且组件内部声明接收了的属性
        .context:上下文对象
            ·attrs:值为对象，包含: 组件外部传递过来，但没有在props配置中声明的属性,相当于this.$attrs.
            ·slots: 收到的插槽内容,相当于 this.$slots.
            emit: 分发自定义事件的函数,相当于 this.$emit


## 7.计算属性与监视
    1.computed函数
        .与Vue2.x中computed配置功能一致
        .写法
            import {computed} from 'vue
            setup(){
                //计算属性一简写
                let fullName = computed(()=>{
                    return person.firstName + "-" + person.lastName
                }
                20//计算属性一完整
                let fullName = computed({
                    get(){
                        return person.firstName +  .+ person.lastNameset(value)
                    },
                    set(){
                        const nameArr = value.split(')
                        person.firstName = nameArr[0]
                        person.lastName = nameArr[1]
                    }
                })


## 3.watchEffect函数
    .watch的套路是: 既要指明监视的属性，也要指明监视的回调。
    .watchEffect的套路是: 不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性
    .watchEffect有点像computed:
        .但computed注重的计算出来的值(回调函数的返回值)，所以必须要写返回值
        .而watchEffect更注重的是过程(回调函数的函数体)，所以不用写返回值
    //watchEffect所指定的回调中用到的数据只要发生变化，则直接重新执行回调。watchEffect(()=>{
        const x1 = sum.value
        const x2 = person.age
        console.log("watchEffect配置的回调执行了")
    })               

##  Vue3生命周期 
    .Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名:
        beforeDestroy改名为 beforeUnmount
        destroyed 改名为unmounted
    Vue3.0也提供了 Composition API形式的生命周期钩子，与Vue2.x中钩子对应关系如下:
        .beforeCreate ===> setup()
        .created =======>setup()
        .beforeMount ===>onBeforeMount
        .mounted =======>onMounted
        .beforeUpdate ===> onBeforeUpdate
        .updated =======> onUpdated
        .beforeUnmount==>onBeforeUnmount
        .unmounted=====>onUnmounted


## 9.自定义hook函数
    .什么是hook? -本质是一个函数，把setup函数中使用的Composition API进行了封装
    .类似于vue2.x中的mixin。
    .自定义hook的优势: 复用代码让setup中的逻辑更清楚易懂

## 10.toRef
    .作用: 创建一个 ref 对象，其value值指向另一个对象中的某个属性
    .语法: const name = toRef(person,'name')
    .应用: 要将响应式对象中的某个属性单独提供给外部使用时
    .扩展: toRefs 与toRef 功能一致，但可以批量创建多个ref 对象，语法:
    toRefs(person)


## 三、其它 Composition API
    1.shallowReactive 与 shallowRef
        .shallowReactive: 只处理对象最外层属性的响应式 (浅响应式)
        .shallowRef: 只处理基本数据类型的响应式,不进行对象的响应式处理。
        .什么时候使用?
            .如果有一个对象数据，结构比较深,但变化时只是外层属性变化 ===> shallowReactive。
            .如果有一个对象数据，后续功能不会修改该对象中的属性，而是生新的对象来替换 ===> shallowRef.


    2.readonly 与 shallowReadonly
        .readonly: 让一个响应式数据变为只读的 (深只读)
        .shallowReadonly: 让一个响应式数据变为只读的 (浅只读)
        .应用场景:不希望数据被修改时

    3.toRaw 与 markRaw
        .toRaw:
            .作用:将一个由reactive 生成的响应式对象转为普通对象
            .使用场景:用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新
        .markRaw:
            .作用: 标记一个对象，使其永远不会再成为响应式对象
            .应用场景:
                1.有些值不应被设置为响应式的，例如复杂的第三方类库等
                2.当染具有不可变数据源的大列表时，跳过响应式转换可以提高性能

## 4.customRef
    .作用:创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制。
    .实现防抖效果:
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
        
