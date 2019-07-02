###指令

1. vue指令是带有v-前缀的特殊特性
2. 指令特性的值预期是单个javascript表达式，表达式的值改变，会响应式作用于DOM



### 指令参数

1. 部分指令可以接受一个参数，在指令后以冒号表示，如v-bind可以用于**响应式的更新HTML特性，或者监听DOM事件**
2. 指令也可以接受一个javascript表达式作为指令**动态参数**，动态参数的值是js表达式的求值结果，**求值结果必须为string 或者null，null可以显性的移除绑定**，其他类型求值结果都会报warning，**js表达式中有一定的语法约束，不可使用空格和引号**，放在HTML特姓名中是无效的，会报错
3. 如果在DOM中使用模板（<u>直接在HTML中使用模板</u>），要注意浏览器会把所有特姓名强制转化为小写。

```vue
<a v-bind:href="url"></a>
<a v-on:click="OnClink"></a>
<button :[attrsName]="true">anniu</button>
<button :[two+one]="true">anniu</button>
<button :[two + one]="true">anniu</button> //报错
<button :[two+'1']="true">anniu</button> //报错
<script>
export default {
  data(){
    return {
      one:'disabled',
      two:'',
      attrsName:[]//[Vue warn]: Invalid value for dynamic directive argument (expected string or null)
    }
  }
}
</script>
```



### 指令修饰符

1. 修饰符以`.`指明的特殊后缀
2. 用于指出一个指定以某种特殊方式绑定
3. 