# Jqery中的AJAX #

----------


ajax一个前后台配合的技术，它可以让javascript发送http请求与后台通信，获取数据和信息。

在jquery中将它封装成了一个函数`$.ajax()`，使用这个函数将可以执行ajax请求

常用参数：
1、`url` 请求地址
2、`type` 请求方式，默认是`GET`，常用的还有`POST`
3、`dataType` 设置返回的数据格式，常用的是'json'格式，也可以设置为'html'
4、`data` 设置发送给服务器的数据
5、`success` 设置请求成功后的回调函数
6、`error` 设置请求失败后的回调函数
7、`async` 设置是否异步，默认值是`true`，表示异步

使用方法
```
// 新方式(推荐)
$.ajax({
    url: '/change_data',
    type: 'GET',
    dataType: 'json',
    data:{'code':300268}
})
.done(function(dat) {
    alert(dat.name);
})
.fail(function() {
    alert('服务器超时，请重试！');
});

// 旧方式
$.ajax({
    url: '/change_data',
    type: 'GET',
    dataType: 'json',
    data:{'code':300268}
    success:function(dat){
        alert(dat.name);
    },
    error:function(){
        alert('服务器超时，请重试！');
    }
});
```

## 局部刷新和无刷新 ##
ajax可以实现局部刷新，也叫做无刷新，无刷新指的是整个页面不刷新，只是局部刷新，ajax可以自己发送http请求，不用通过浏览器的地址栏，所以页面整体不会刷新，ajax获取到后台数据，更新页面显示数据的部分，就做到了页面局部刷新。