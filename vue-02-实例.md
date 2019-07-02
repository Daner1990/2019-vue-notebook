### 创建Vue实例

1. vue收到mvvm模型启发，所以在文档中使用vm（ViewModel）缩写表示Vue实例
2. 所有的Vue组件都是Vue实例，并接受相同的选项对象（根实例特有选项除外）
3. 当一个Vue实例被**创建时**，他将data对象中所有的属性加入到Vue的**响应式系统**中。这些属性变化，视图会产生响应，更新匹配为新值
4. **只有在当实例被创建时data中存在的属性才是响应式的！**实例创建完成后添加的新属性的变更不会触发任何视图的更新
5. 所有需要被使用的属性，需在一开始设定，并赋予一些初始值即可



### Vue实例生命钩子函数

1. 给用户在不同阶段添加自己代码的机会
2. 生命周期钩子的this上下文指向调用他的Vue实例
3. **不要在选项属性或者回调上使用箭头函数，箭头函数没有this，this会作为变量一直向上级词法作用域查找直到找到为止，经常报错**



####Object.freeze()对属性的影响：

```vue
<template>
  <div id="slide">
    {{data.slide}}
    <div @click="changeSlide">changeSlide</div>
  </div>
</template>

<script>
var Mdata = { slide: " i am slide" };

// Object.freeze(Mdata) //系统无法在追踪Mdata的变化，对应data不会再更新

export default {
  name: "slide",
  components: {},
  data() {
    return {
      //   data : Mdata
      data: ""
    };
  },
  mounted() {
    // Object.freeze(Mdata) //worked cannot change
    this.data = Mdata;

    // Object.freeze(Mdata) //not work,can change data
    // this.data = Object.assign({},Mdata)

    console.log(this.data === Mdata);
    console.log(this.$el === document.getElementById("slide"));
  },
  methods: {
    // changeSlide:()=> {
    changeSlide(){
      this.data.slide = this.data.slide
        .split("")
        .reverse()
        .join("");
      console.log(Mdata.slide);
    }
  }
};
</script>

<style>
/* i am slide style */
</style>

```

