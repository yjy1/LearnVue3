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
            proxy.name = 'tom!