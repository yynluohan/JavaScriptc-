# js刷新当前页的几种方式 #

## 目录 ##

 1. [reload方法](#href1)
 2. [replace方法](#href2)
 3. [其他手动刷新的方法](#href3)
 4. [自动刷新页面的方法](#href4)
 5. [页面自动跳转](#href5)


### <a name='href1'>reload方法</a> ###

reload ： 强制浏览器刷新当前页面，相当于浏览器上的刷新页面按钮。

语法：location.reload([bForceGet])  

bForceGet为可选参数，默认为false(从客户端里取缓存页)，如果设置true的话，则以GET的形式，
从服务端取当前页面，相当于客户端点击F5（"刷新"）

```js
window.location.reload()
```


### <a name='href2'>replace方法</a> ###

replace方法可用于新文档取代当前文档。

```js
window.location.replace("/login")
```

注意：window.location.replace 与 window.location.href 有个不同的地方。
如果使用window.location.replace跳转的话，它将新页面的地址在history的地址列表中删除，
    因此使用back或go函数无法导航。
如果使用window.location.href 新页面的地址将被加入history的地址列表中，因此可以使用back或go函数导航。


### <a name="href3">其他手动刷新的方法</a> ###

```
  1. history.go()
  2. location = location
  3. location.assign(location)
  4. document.execCommand('Refresh')
  5. window.navigate(location)
  6. document.URL=location.href
```

### <a name="href4">自动刷新页面的方法</a> ###

<head>中设置：

```
<meta http-equiv="refresh" content="20"/>
```

也可使用js实现
```js
function reflesh() {
  window.location.reload()
}
setTimeout(reflesh,1000), //每隔一秒刷新
```


### <a name="href5">页面自动跳转</a> ###
<head>中设置：

```
<meta http-equiv="refresh" content="20;url="https://www.baidu.com">
//content： 20秒后跳转到https://www.baidu.com
```
