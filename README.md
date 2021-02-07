# module_6
响应式、虚拟 DOM、模板编译和组件化

## 请简述 Vue 首次渲染的过程
-  在Vue渲染之前需要创建Vue构造函数,初始化它的实例成员与静态成员然后在webplatform中为Vue添加web平台下会使用到的方法,`$mount`与`__patch__`方法
- 在上一步基础上拥有了一个可用的Vue类,通过`new Vue({...}).$mount('#app')`可以生成dom元素并挂载
  - 判断用户是否传入render函数,如果没有传入就找到传入的模板编译为render函数,保存在`vm.$options`中
  - 然后通过`mountComponent(this,el)`进行挂载
  - `mountComponent`的核心是创建`updateComponent`和`渲染watcher`,将`updateComponent`传递进去,在此之前会调用beforeMount钩子函数,之后会调用mounted钩子函数
  - 在`渲染watcher`创建过程中执行构造函数时,由于lazy属性默认为false此时会直接调用`this.get()`方法
  - 在get方法会调用`updateComponent`,此时`updateComponent`会被保存在watcher的getter属性中
  - `updateComponent`中通过`vm.render`函数生成vnode,这里的render就是用户传入或模板编译的
  - 生成vnode之后将其传递给`vm.update()`生成真实的dom元素,并挂载在页面中,其中的核心是调用web平台传入的`__patch__`方法
流程图
![image-20201023115156550](module_6/src/image/image-20201023115156550.png)
