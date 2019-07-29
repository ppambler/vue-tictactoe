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
    },
    isOver: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      a: false,
      text: '',
      temp: false
    }
  },
  created() {
    let _this = this
    this.eventBus.$on('update:has',function(n) {
      _this.temp = n
    })
  },
  methods: {
    xxx() {
      if(this.text !== '') {
        return
      }
      if(this.isOver) {
        return
      }
      this.a = true
      this.temp ? this.text = '○': this.text = 'x'
      this.eventBus.$emit('update:has', !this.temp,this.name,this.text)
    }
  },

};
</script>

<style scoped>
.cell {
  box-sizing: border-box;
  padding-bottom: 20px;
  color: black;
  border: 1px solid black;
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 80px;
}
</style>