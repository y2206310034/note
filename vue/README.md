## VUE  

### Why Use

1. 性能更好

    我们都知道操作dom是极其消耗性能的,但是因为什么消耗性能可能就是一知半解了,下边我具体写出了为什么消耗性能

        1. JS和Dom是两种东西,js与dom的每次连接都需要消耗性能
           首先我们需要知道js与dom的关系到底是怎样的,在学到这一块之前我一直以为dom就是js中的一部分,其实不然,DOM是一个独立于语
           言(与语言无关的)的，用于操作XML和HTML文档的程序接口(API),它在浏览器中的接口是用JavaScript来实现的,客户端脚本编程
           大多数都是在和底层文档打交道
           浏览器中通常会把DOM和javascript独立实现.
        2. 操作dom会导致重排和重绘
            当DOM的变化影响了元素的几何属性（宽和高）,浏览器需要重新计算元素的几何属性,同样其他元素的几何属性和位置也会因此受
            到影响。浏览器会使渲染树中受到影响的部分失效,并重新构造渲染树。这个过程称为重排,完成重排后,浏览器会重新绘制受影响的
            部分到屏幕中,该过程称为重绘.
    
    vue的核心是虚拟dom,使用虚拟dom可以减少dom的操作,从而提升应用的性能.

    dom的操作是昂贵的,js的运行效率更高,将dom对比放在js层,减少dom操作,效率更高.

    vue中虚拟dom就是在js中比较dom的修改,只改变那些需要改动的dom元素,大大减少了dom的操作.

2. 视图数据分离

    只用关心数据的变化，处理数据就是处理数据，显示视图就是显示视图，分层来做，这样更符合思考的逻辑 

    如果用原生js或jq的话首先需要在js中获取到dom,然后修改数据 在渲染dom


3. 维护成本低

    vue的代码量更少,逻辑更清晰

### What is Vue

    Vue是一套用于构建用户界面的渐进式框架,Vue 被设计为可以自底向上逐层应用.Vue 的核心库只关注视图层,不仅易于上手,还便于与第三
    方库或既有项目整合.

    Vue是一个MVVM框架
    M:model(数据),
    V:view(视图),
    VM:ViewModel(相当于一个桥梁)

    model通过ViewModel中的Data Bindings 影响view
    view通过ViewModel中的Dom  Listeners 影响model



### 常见的问题


#### v-bind和v-model的区别

    1.v-bind用来绑定数据和属性以及表达式，缩写为'：'
    2.v-model使用在表单中，实现双向数据绑定的，在表单元素外使用不起作用

#### 什么是MVVM
    MVVM 是 Model-View-ViewModel 的缩写。mvvm 是一种设计思想。Model 层代表数据模型，也可以在 Model 中定义数据修改和操作的业
    务逻辑；View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来，ViewModel 是一个同步 View 和 Model 的对象。

    在 MVVM 架构下，View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向
    的， 因此 View 数据的变化会同步到 Model 中，而 Model 数据的变化也会立即反应到 View 上。

    ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因
    此开发者只需关注业务逻辑，不需要手动操作 DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理

#### MVVM与MVC的区别
    mvc 和 mvvm 其实区别并不大。都是一种设计思想。主要就是 mvc 中 Controller 演变成 mvvm 中的 viewModel。
    mvvm 主要解决了mvc 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。和当 Model 频繁发生变化，
    开发者需要主动更新到 View 。

#### 说一说new Vue()在各个生命周期做了那些事

1. 初始化事件处理函数（$on, $emit,$delete）,生命周期函数，里面还不能访问data，methods，computed
2. 触发beforeCreate生命周期函数，在这个阶段一般声明不被相应的元素，一般不会用到
3. 初始化data，computed，methods。
4. 触发created函数，在这个阶段data，computed，methods都可以正常的访问。通常在这个阶段做一些初始化的工作，发送少量的ajax请求用于初始化，过多请求会导致页面加载慢。
5. 判断是否有el属性，如果有，判断是否有template属性，如果有就用template属性作为模板，没有的话使用el选择器所选择元素以及所有子元素构成模板进行解析编译(如果没有el属性，当执行vm.$mount(el)才会执行).
6. 触发beforeMount函数。
7. 用template编译好的AST(抽象语法树),配合render函数,重新构建DOM树，并替换原有的DOM
8. 触发mounted函数，至此当前Vue实例挂载完成。但不意味着子组件会挂载完成。这个函数通常用于ajax请求，做其他的数据交互。
9. 当数据发生变化时候，无论哪个数据，都会触发beforeUpdate函数，然后经过VDOM 对比，diff算法，找到VDOM差异，进行局部重新渲染。之后触发updated函数，在这两个函数最好不要进行数据操作，会导致死循环。
10.当触发vm.$destory()函数，或者组件销毁是会先后触发 beforeDestroy 和 destroyed函数。

