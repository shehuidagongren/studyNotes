





报错解决

## 一、类型一

### 1.Vue语法

#### 1.methods==>method

 method写成了methods

报错方式1

```
Request failed with status code 404 AxiosError: 
Request failed with status code 404    at settle 
(webpack-internal:///./node_modules/axios/lib/core/settle.js:24:12)    
at XMLHttpRequest.onloadend 
(webpack-internal:///./node_modules/axios/lib/adapters/xhr.js:109:66)
```

报错方式2

```
AxiosError {message: ‘Request failed with status code 404‘, name: ‘AxiosError‘……
```

**报错原因**：Vue JavaScript语法中周期函数 method写成了methods

**解决方法**：methods改成method



#### 2.this无法指向data中的数据

预想在Vue创建页面时接收后端数据，然后渲染到页面。使用data进行数据绑定，可是数据修改不成功。

Vue中使用mounted和created时，this无法指向data中的数据

```ma
vue.runtime.esm.js:3049  TypeError: this.getUserinformation is not a function     at VueComponent.mounted (userManagement.vue:258:1)     at invokeWithErrorHandling (vue.runtime.esm.js:3017:1)
```

**报错原因**：最开始的理解中this.userManagement指的是Vue中的数据userManagement，事实并不如此，这里的this代指window对象而不是Vue对象，所以真正找的是window对象下的userManagement，但是window下没有userManagement，所以就报错了。

**解决方法**：把指向vue对象保存给一个变量that，在后面引用that来修改数据即可



## 2.跨域问题

1.vue.config.js配置

刷新页面弹出Cannot GET /homeHome

![image-20231124142156869](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124142156869.png)

**报错原因**：空路径错误

**解决方法**：将vue.config.js里的publicPath:""改成 publicPath: "/",

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
 transpileDependencies: true,
 lintOnSave: false,//关闭语法检查
 publicPath: "/",
   devServer: {
 //   // 跨域问题解决 代理（关键部分）
   proxy:  'http://localhost:8080', // 注意！此处为后端提供的真实接口
 }
})
```

