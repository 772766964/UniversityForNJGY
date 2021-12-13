# axios

## 什么是同源？

在请求网络路径的时候，主机地址不一样，ip地址（主机号），端口不一样都叫不同源。这种现象叫做跨域，因此我们需要允许跨域去请求数据。

## 什么是axios

axios是基于romise对ajax的封装

## axios的基本使用

//使用默认方式发送无参请求

``` javascript
axios({
    url:'api地址',
    //如果不写下面一行默认就是get，
    method:'get'
}).then(res=>{
       console.log(res);
}).chtch(err=>{
    console.log(err)
})
```

//使用get方式进行有参请求

``` html
axios({
    url:'api地址？id=1 ',
    //如果不写下面一行默认就是get，
    method:'get'
}).then(res=>{
       console.log(res);
})
```

使用get方法有参请求

``` js
<script>
    axios.get(url,{params:{id:1,name:'a'}}).then(res=>{
    console.log(res)
}).catch(err=>{
    console.log(err);
})
</script>
```



//使用post方式无参请求

``` html
axios({
    url:'api地址',
    //如果不写下面一行默认就是get，
    method:'post'
}).then(res=>{
       console.log(res);
})
```

使用post方法有参请求

``` js
<script>
    axios.get(url,"id=1&name=z").then(res=>{
    console.log(res)
}).catch(err=>{
    console.log(err);
})
</script>
```



