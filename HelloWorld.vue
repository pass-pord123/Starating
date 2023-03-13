<template>
  <div>
    <h1>
      <strong>{{ name }}</strong>
    </h1>
    <div class="star">
      <span
        v-for="i of 5"
        :key="i"
        :class="{ checked: ischecked(i) }"  
        @click="clickstar(i)"
        >★</span
      >
      <!-- checked是class的名字，用来控制元素字体是否为红色： 他是否加到span的class里面的话 要看  ischecked这个函数执行后返回的值是否为true
      true的话就 把checked这个类名加到 span的class里面   在最下面可以看到 如果有checked这个类名 他的字体就会变成红色 -->
      <!-- clickstar 是一个函数 因为上面用了v-for 他的参数就是 对应的数字 比如 i如果是1 代表的就是第一颗星 4就是第四课星星  -->
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: ["modelValue", "name"],
  emits: ["update:modelValue"],
  // 老师说过 如果父组件用v-model给儿子传值， 然后子组件（当前组件）的props只能写（'modelValue'）来代表父组件传来的值
  //这个modelValue  一个单词都不能错 不能用其他的名字，写死的。 
  // props 相当于接受的意思， 接收来自父亲传来的值
  // emits 如其名  发射，   发射子组件的信息给父组件
  methods: {
    clickstar(i){
      this.$emit('update:modelValue', i)
      //每次点击星星 都会触发这个函数  这个函数的参数i就是 第几课星星的意思
      // 然后这个this.$emit就是给爸爸组件发送信息； 第一个参数是爸爸接受的 自定义事件 （ @abc = 'xxx'） 那个@代表自定义事件=》针对子组件的时候是这样说（细节另外问我）
      // 第二个参数就是 （ @abc = 'xxx'）里面xxx的参数   一般 xxx 就是 一个函数，在爸爸组件methods 里面定义的一个函数
      //因为爸爸组件用v-model  所以$emit 第一个参数也是写死的  必须是 'update:modelValue'
      // 每次执行clickstar这个函数 爸爸里面的对应的product里面的星星就会变化；
      // 变化之后 vue的数据是响应式的 检测到变化后  页面就会针对变化的数据进行刷新； 然后子组件这里获得新的modelValue的值
      // 然后触发ischecked 重新执行  就会变成你点击后的星星哪些红色 哪些黑色
    },
    ischecked(i){
      return this.modelValue>= i? true:false
      // thIs.modelValue 是爸爸传过来的值， 这里的意思就是  i是代表 当前星星的序号  i=1 就是第一颗星星 以此类推
      // 这里的意思 就是爸爸传过来的star 的值 如果大于i  就return true 给上面的:class="{ checked: ischecked(i) }" 
      // 如果checked 看到是true  他就会给目标元素class加个checked   自然而然  他就变红了。
      //以此类推
    }
  },
};
</script>

<style scoped>
.checked {
  color: red;
}
.star:hover {
  color: red;
}
</style>
