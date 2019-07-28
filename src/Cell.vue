<template>
    <div class="cell" v-on:click="xxx">
      <template v-if="a">{{text}}</template>
      <template v-else></template>
    </div>
</template>

<script>
export default {
  name: "cell",
  inject: ['eventBus'],
  props: {
    name: {
      type: String
    }
  },
  data() {
    return {
      a: false,
      text: 'x',
      temp: false
    }
  },
  created() {
    // console.log(this.name)
    let _this = this
    this.eventBus.$on('update:has',function(n) {
      // 这个事件的监听先于父组件的监听执行
      // console.log(this) //这个this是eventBus 这个Vue实例呀！
      // console.log(_this)
      // console.log(`${_this.name}说「${n}」被点击了`)
      _this.temp = n
    })
  },
  methods: {
    xxx() {
      if(this.temp) {
        this.text = '○'
        this.a = true
      }
      this.a = true
      this.eventBus.$emit('update:has', !this.temp)
    }
  },

};
</script>

<style scoped>
.cell {
  box-sizing: border-box;
  padding-bottom: 20px;
  color: red;
  border: 1px solid black;
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 80px;
}
</style>