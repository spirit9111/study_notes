# ES6基本常识 #

----------

变量定义方式:
`var`:支持预解析,可以修改
`let`:不支持预解析,可以修改
`const`:不支持预解析,**常量**不能修改.

箭头函数
用于解决this指向混乱的问题,可以看成另一种匿名函数
```
// 定义函数的一般方式
function fnRs(a,b){
    var rs = a + b;
    alert(rs);
}
fnRs(1,2);        

// 通过匿名函数赋值来定义函数
var fnRs = function(a,b){
    var rs = a + b;
    alert(rs);
}
fnRs(1,2);

// 通过箭头函数的写法定义
var fnRs = (a,b)=>{
    var rs = a + b;
    alert(rs);
}        
// fnRs(1,2);

// 一个参数可以省略小括号
var fnRs2 = a =>{
    alert(a);
}
fnRs2('haha!');


// 箭头函数的作用，可以绑定对象中的this
var person = {
    name:'tom',
    age:18,
    showName:function(){
        setTimeout(()=>{
            alert(this.name);
        },1000)            
    }
}
person.showName();
```