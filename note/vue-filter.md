### 过滤器
用于文本格式化，数组数据的过滤和排序
### 全局过滤器
```js
Vue.filter('',function(){})
```
### 局部过滤器
```js
new Vue({
    el:"#app",
    filters:{
        uppcase(){
            
        }
    }
})
```
### 使用地方
管道符号添加到表达式后面
1. 插值表达式
2. v-bind表达式

### 过滤器的参数 (管道传入)
```
<body>
    <div id="app">
        <!-- 在这里使用管道符号传入第一个参数进入format -->
        <p>{{filename | format('vue',suffix)}}</p>
    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>
        // value由管道传入
        Vue.filter('format', function(value, prefix, suffix) {
            if (!value) return '';
            value = value.toString();
            return prefix + '-' + value + '.' + suffix;
        });
        const app = new Vue({
            el: "#app",
            data: {
                filename: "filters",
                suffix: "js"
            }
        });
    </script>
</body>
```

### 过滤器串联：利用管道进行参数的传递
<p>{{message | uppercase() | reverse()}}</p>
```js
<body>
    <div id="app">
        <p>{{message | uppercase() | reverse()}}</p>
    </div>
    <script src="../node_modules/vue/dist/vue.js"></script>
    <script>
        Vue.filter('uppercase', function(value) {
            if (!value) return '';
            value = value.toString();
            return value.toUpperCase();
        });
        Vue.filter('reverse', function(value) {
            if (!value) return '';
            value = value.toString();
            return value.split('').reverse().join('');
        });
        const app = new Vue({
            el: "#app",
            data: {
                message: "Hello World!"
            }
        })
    </script>
```
### 总结
- Vue中的过滤器其实就是一个 “函数” , 可以根据管道符号 “|” 传入第一个值。
- 插值表达式；v-bind表达式；过滤器一定要返回值
- 借助管道可以实现串联
