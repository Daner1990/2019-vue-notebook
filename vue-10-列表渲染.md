可以支持数值，对象循环

```vue
<template>
  <div>
    <button @click="changeForOpt">changeForOpt</button>
    <div v-for="(item ,index) in items" :key="'item-'+index">
      <p>{{index}}:{{item}}</p>
    </div>
    <!-- <div v-for="(item ,index) of items">
            <p>{{index}}:{{item}}</p>
    </div>-->
    <!-- object.kyes()遍历对象，但是无法保证在所有浏览器的表现一样 -->
    <div v-for="(item ,key,index) in objects" :key="'object-'+index">
      <p>{{index}}:{{key}}-{{item}}</p>
    </div>
    <!-- <div v-for="(item ,key,index) of objects">
            <p>{{index}}:{{key}}-{{item}}</p>
    </div>-->
  </div>
</template>

<script>
export default {
  name: "contents",
  components: {},
  props: ["fvalue"],
  data() {
    return {
      items: [1, 2, 3, 4, 5, 6],
      objects: {
        obj1: "val1",
        obj2: "val2",
        obj3: "val3",
        obj4: "val4",
        obj5: "val5"
      }
    };
  },
  computed: {},
  watch: {},
  methods: {
    changeForOpt() {
      this.items[1] = "直接修改item的值"; //不是响应式的
      this.items.length = 3; ///不是响应式的
      //this.objects.xx="xxx"///不是响应式的
      //vue将被监听的数组的变异方法进行了包裹，所以他们会触发视图更新
      //变异方法，直接改变数组：push pop shift unshift sort reverse
      //非变异方法，生成新数组：filter concat slice
      this.items.push("newpush"); //响应式，会顺带上以上非响应式修改生效
      this.items = this.items.filter((item, value) => {
        return value > 2;
      });
    }
  }
};
</script>

<style>
</style>


```



###数组的响应式

1. vue将被监听的数组的变异方法进行了包裹，所以他们会触发视图更新
2. 变异方法，直接改变数组：push pop shift unshift sort reverse
3. 非变异方法，生成新数组：filter concat slice
4. vue不能监听到直接通过索引设置一个数组项
5. vue不能监听对数组长度的修改



### 对象的响应式

1. vue不能检测到对象属性的添加或者删除
2. 对于已经创建的实例，vue不允许动态添加根级别的响应式属性
3. 但是可以通过Vue.set 或者vm.$set来向嵌套对象添加响应式属性
4. 如果要为已有对象赋值多个新属性可以用Object.assign()或者_.extend()

