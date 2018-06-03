# vue.js #

----------
vue.js文档:[https://cn.vuejs.org/v2/guide/](https://cn.vuejs.org/v2/guide/)

创建vue对象方式:
```
var vm = new Vue({
        el:'#app',
        data:{message:'hello world!'},
        methods:{
            fnA:function(){
        ...}
    }
});
```
`el`对应一个html标签,这个标签内就会被vue对象都接管,都可以操作
`data`保存了所有能被vue对象使用的属性
`methods`保存了所有能被vue对象使用的方法
`computed`计算属性,可以将模板中复杂的逻辑封装在这里.
`watch`侦听属性,侦听属性值的变化,当侦听的属性发生改变时,自动执行相应的函数.
`filter`过滤器,常用于对文本的格式化
`mounted`实例挂载到dom之后被调用，可以当成是vue对象的ready方法来使用，一般用它来做dom的初始化操作。


vue.js模板语法:

向标签内插入数据:

使用`{{ data中的变量名 }}`,例如`<span>消息: {{ message }}</span>`

还支持
```
{{ number + 1 }}  # 进行简单的计算
{{ ok ? 'YES' : 'NO' }}  # 三元运算式
{{ message.split('').reverse().join('') }}  # 相应js操作
```

操作标签属性:

使用`v-` 指令来进行操作,可以直接操作data中定义的变量
常用的指令
`v-bind:` 用于操作一般的属性简写为`:`,例如`<a v-bind:herf:'#'>`/`<a :herf:'#'>`
`v-on` 用于操作事件简写为`@`,`.stop`阻止冒泡,例如`<button v-on:click="fnChangeMsg">按钮</button>`/`<button @click="fnChangeMsg">按钮</button>`
`v-if` 控制标签创建和销毁,使用bool进行判断,ture创建,false销毁
`v-else-if`同上
`v-else`同上
`v-show`控制标签显示还是隐藏
`v-for`循环遍历,第一个为value,第二个参数(可选)为索引或者key`<div v-for=(i,index) in aList>{{ i }}{{ index }}</div>`
`v-model`双向数据绑定,一般用于`<input>`,绑定多选框时必须用`[]`

```
<div>
	<p v-show="t">qqq</p>
	<p v-if="t">www</p>
	<p v-else-if="f">eee</p>
	<p v-else="f">rrr</p>
</div>
<script>
	var	vm =new Vue({
		el:'div',
		data:{
			t:true,
			f:false
		}
	})
</script>
```



操作calss属性
```
# 传入一个对象控制class-对象语法(需要判断true/false)
<div v-bind:class="classObject"></div>
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}

# 也可以写作
<div v-bind:class="{active:isActive,'text-danger':hasError }"></div>
data: {
  isActive: true,
  hasError: false
}

#也可以使用-数组语法(默认表示and关系)
<div v-bind:class="[activeClass, errorClass]"></div>

# 数组语法需要判断时,使用三元运算表达式进行
<div :class="[bool ? activeClass : '', errorClass]"></div>
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

````

也可以操作style属性
```
# 对象语法
<div v-bind:style="{color: activeColor, fontSize: fontSize + 'px' }"></div>
data: {
  activeColor: 'red',
  fontSize: 30
}

<div v-bind:style="styleObject"></div>
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}

# 数组语法
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

过滤器的两种定义方式

```
使用方式
<!-- 在双花括号中 -->
{{ prize | RMB }}

<!-- 在v-bind中 -->
<div v-bind:id="rawId | formatId"></div>

#  定义方式1:定义在vue实例对象中--局部过滤器
filters:{
  RMB:function(value){
    if(value=='')
    {
      return;
    }
    return '¥ '+value;
  }
}

#  定义在vue实例之前--全局过滤器
Vue.filter('Yuan',function(value){
  if(value=='')
  {
    return;
  }
  return value+'元';
});

```

## vue中的ajax操作 ##
vue.js没有集成的ajax功能,推荐使用**axios.js**库
axios.js基本语法(基本和jquery中的ajax相同):
```
var vm = new Vue({
	el: 'aaa',
	data: {bbb: []},
	mounted: function () {
		axios({
			method: 'post',
			url: '/user/12345',
			data: {
				firstName: 'Fred',
				lastName: 'Flintstone'
			}.then(function (response) {
				console.log(response);
			}).catch(function (error) {
				console.log(error);
			})
		})
	}
})
```