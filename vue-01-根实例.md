

若页面尚未挂载任何vue实列，输出页面如下：

```html
<html lang="en"><head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="/favicon.ico">
    <title>vue-base-practice</title>
  <link href="/app.js" rel="preload" as="script"><style type="text/css">
/* i am singlePage style */
</style><style type="text/css">
/* i am content style */
</style><style type="text/css">
/* i am slide style */
</style></head>
  <body data-feedly-extension-follow-feed="1.0.3" data-feedly-mini="yes" cz-shortcut-listen="true">
    <noscript>
      <strong>We're sorry but vue-base-practice doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  <script type="text/javascript" src="/app.js"></script>

<div id="feedly-mini" title="feedly Mini tookit"></div></body></html>
```

vue默认会在body下生成一个id为app的元素

```javascript
import Vue from 'vue'
import singlePage from './singlePage.vue'
import Contents from './content.vue'
import Slide from './slide.vue'

Vue.config.productionTip = false

var vueRoot = new Vue({
  // el:'#app',
  render: h => h(singlePage),
})
.$mount('#app')

// 
var bodyvue = new Vue({
  // el:'#content',
  render: h => h(Contents),
})
// .$mount('#contents')

var slidevue = new Vue({
  el:'#slide',
  render: h => h(Slide),
})
// .$mount('#slide')
```



### 根元素挂载

	1. 提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例。
 	2. 所以根元素必须挂载在已存在的DOM元素`#app`上，因为提供的元素只能作为挂载点，**所有的挂载元素最终会被 Vue 生成的 DOM 替换**。因此不能挂载 root 实例到 `<html>` 或者 `<body>` 上。
 	3. 若在实例化中以`el`指定了挂载元素，存在这个选项，**实例将立即进入编译过程**，否则，需要**显式调用 `vm.$mount()` 手动开启编译**。
 	4. 在实例挂载之后，元素可以用 `vm.$el` 访问



-----





