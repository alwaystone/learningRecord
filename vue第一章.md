1.什么是MVVM?
    Model:负责数据存储
    View:负责页面展示
    View Model:负责业务逻辑处理,对数据进行加工后交给视图展示

MVC模式(设计模式,前后端都有的模式)
    M->model->模型->数据(js变量)
    V->View->视图->用户所见页面
    C->control->控制器->事件交互->如何根据视图与用户交互后改变数据



v-if v-else 会直接删除一个元素或者插入一个元素

v-show 会将display设置为none 

for循环带有index的写法 其中必须设置:key 只有设置才会重新渲染  否则会原有的只是修改值
<li v-for="item,index in students">
    {{index}}---{{item}}
</li>

v-once 绑定值  但是只插入一次 不随着js改变而改变
<h1 v-once>{{msg}}</h1>

computed计算属性 与method有一定的区别  computed只能用作属性用  计算属性是基于它们的响应式依赖进行缓存的
计算属性默认只有 getter，不过在需要时你也可以提供一个 setter：

// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
现在再运行 vm.fullName = 'John Doe' 时，setter 会被调用，vm.firstName 和 vm.lastName 也会相应地被更新。


checkbox的使用
<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
<label for="jack">Jack</label>
<input type="checkbox" id="john" value="John" v-model="checkedNames">
<label for="john">John</label>
<input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
<label for="mike">Mike</label>
<br>
<span>Checked names: {{ checkedNames }}</span>
new Vue({
  el: '...',
  data: {
    checkedNames: []
  }
})