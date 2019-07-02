<u>在v-if v-else的切换中，vue的机制是高效的渲染元素，所以vue的通常做法是复用已有的元素，而不是重头开始渲染</u>

这样做可以让vue渲染变得特别快，还有一些其他的好处，比如两个条件判断中使用了相同的元素，比如input，input在条件切换中并不会被替换掉，只是会替换他的属性。

但是这种情况也不是总符合我们的实际需求，我们很多时候**需要保证元素的唯一性**

**vue提供了key属性来保证两个元素是完全独立的，不要复用他们**

```vue
<template>
<div>
  <div id="app00">
    <button @click="changeIfOpt">changeIfOpt</button>
    <template v-if="changeIf">
      <!--输入value会保留 input被复用-->
      <input placeholder="true"/>
      <!--输入value会清空 input具有唯一性-->
      <input placeholder="true" key='1'/>
    </template>
    <template v-else>
			<!--输入value会保留 input被复用-->
      <input placeholder="false"/>
			<!--输入value会清空 input具有唯一性-->
      <input placeholder="false" key='2'/>
    </template>
    </div>
</div>
</template>

<script>

import HelloWorld from './components/mclass.vue'

export default {
  name: 'contents',
  components: {
    HelloWorld
  },
  data(){
    return {
      value:'',
      changeIf:true,
    }
  },
  methods:{
    changeIfOpt(){
      this.changeIf = !this.changeIf
    }
  }
}
</script>

<style>
/* i am content style */
</style>

```





tips：不推荐v-if 和v-for一起使用，如果一起使用v-for的优先级更高