1. 说说你对vue生命周期的理解
   * vue的生命周期可以分为4个阶段，创建前后、载入前后、更新前后、销毁前后
        * 创建前后：在beforeCreated阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化；created阶段：vue实例数据data有了，$el还没有。
        * 挂载前后：在beforeMounted阶段，vue实例的$el和data都已经初始化了，但还是挂载在虚拟dom上，data.message还未替换；在mounted阶段，vue实例挂载完成，data.message成功渲染。
        * 更新前后： 当data变化时，会触发beforeUpdate和updated方法。
        * 销毁前后： 在执行destroy方法后，对data的改变不会再触发周期函数，说明此时，vue实例已经解除事件监听以及dom绑定，但dom结构该存在。
        
2. 怎么理解VUEX
   * 用于管理全局的数据，【通过状态<数据源>的集中管理，驱动组件的变化[好比Spring的IOC容器对bean的集中管理]】
   * 状态集中放置state中，改变状态的方式是提交mutations,这是一个同步事务，异步逻辑应该封装在action中。
   
3. vue-loader是什么？它的用途？
   * 它是webpack的loader，它允许你以一种名为单文件组件<SFCs>的格式写vue组件。
   * 解析.vue文件的一个加载器，跟template/js/style转换成js模块;用途：js可以写es6、style样式可以scss或less，template可以加jade<变体的HTML>等。
   
4. 谈谈你对vue的template的理解
    * 简言之：先转化成AST树，再得到render函数返回的Vnode
    * 详解：通过compile编译器把template编译成AST语法树(abstract syntax tree 即源代码的抽象数据结构树状表达形式)，
      compile是createCompiler的返回值,createCompiler是用以创建编译器的。另外compile还负责合并option
      然后，AST会经过generate(将AST语法树转化成render function字符串的过程)得到render函数，render的返回值是vnode。
      
5. vue的双向数据绑定原理？
    * vue.js是采用数据劫持结合发布者-订阅模式，通过Object.defineProperty()来劫持各个属性的getter、setter，在数据变动时，发布消息给订阅者，触发相应的回调。

6. vue-router有哪几种导航钩子
   三类，一类是全局导航钩子：beforeEach(to,from,next):作用是调转前进行判断拦截、beforeResolve、afterEach；第二类是某个路由独享的导航钩子beforeEnter<直接在router路由配置中使用>，第三类是路由组件上的导航钩子，beforeRouteEnter、beforeRouteUpdate、beforeRouteLeave
        