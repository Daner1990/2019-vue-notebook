在模板中使用表达式十分的便利，但设计在模板中使用表达式的初衷只是为了用于简单的运算，若放入太多的逻辑，会让模板太重，且不好维护，可读性差！

**所以对于复杂的逻辑，我们应该使用计算属性！**

```javascript
  data(){
    return {
      value:'hello th word',
    }
  },
  computed:{
     //计算属性的getter
      revsvalue:function(){
        	//this 指向vm实列，不可以用箭头函数，箭头函数的this会指向undefined
          return this.value.split('').reverse().join('')
      }
  }
```



我们调用方法同样可以达到相同效果，**<u>但是他们之间不同点为计算属性是基于他们的响应式依赖进行缓存的，只有在响应式依赖发生变化时，计算属性才会重新求值，而method在每次触发渲染时，总会去再次执行函数。</u>**

计算属性可以用于依赖性并且大量繁复的计算，如果不希望有缓存，可用方法替代

```vue
<template>
  <div>
    <div id v-if="fvalue">
      {{computedC}}
      {{methodsC()}}
    </div>
  </div>
</template>

<script>
export default {
  name: "contents",
  components: {},
  props: ["fvalue"],
  data() {
    return {
    };
  },
  computed: {
    computedC: function() {
      console.log("computedC", this);
      //return this.fvalue.split('').reverse().join('')
      return Date.now();
    }
  },
  methods: {
    methodsC: function() {
      return Date.now();
    }
  }
};
</script>

```



同时，vue提供了一种通用的方式来观察和响应vue实例上的数据变动，**监听属性（watch）**

但当数据是随着**其他数据变动而变动**时，很容易滥用watch，**但更好的做法是用computed，而不是watch。**

计算属性可以设置setter，一般默认只有getter，通过改变数据源头的形式来改变计算属性



```vue
<template>
  <div>
    <div id v-if="fvalue">
      {{value}}
      {{revsvalue}}
      <button @click="changerevs">change revsvalue</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "contents",
  components: {},
  props: ["fvalue"],
  data() {
    return {
      value: "hello th word"
    };
  },
  computed: {
    revsvalue: {get:function() {
      console.log(this);
      return this.value
        .split("")
        .reverse()
        .join("");
    },set:function(value){
        this.value = value;
    }},
   
  },
  methods: {
    changerevs:function(){
        this.revsvalue="不好啦"
    }
  }
};
</script>

<style>
</style>


```

computed不支持异步操作！

