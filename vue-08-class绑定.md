对于数据绑定，vue对绑定**class & style属性**做了专门的增强，表达式的结果出了能接受字符串之外，还可以接受**对象或者数组**



```vue
<template>
  <div>
    <!--多class更新可以使用computed属性-->
    <div :class="mClass">{{value}}</div>
		<!--color是否存在取决于fvalue的truthness-->
    <div class="commonClass" :class="['bigger',{color:fvalue}]">{{value}}</div>
  </div>
</template>

<script>
export default {
  name: "contents",
  components: {},
  props: ["fvalue"],
  data() {
    return {
      value: "hello the world"
    };
  },
  computed: {
      mClass:function(){
          return {
              "bigger":this.fvalue,
              "color":this.fvalue
          }
      }
  },
  watch: {},
  methods: {}
};
</script>
<style>
.bigger{
    font-size: 13px;
}
.color{
    color: aquamarine
}
</style>


```



tips：在 JavaScript 中，truthy（真值）指的是在布尔值上下文中，转换后的值为真的值。所有值都是真值，除非它们被定义为 假值（即除 false、0、""、null、undefined 和 NaN 以外皆为真值）

