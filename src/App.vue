<template>
  <div>
    <div class="cell" v-on:click="xx(0,true)">
      <template v-if="a[0]">x</template>
      <template v-else></template>
    </div>
    <div class="cell" v-on:click="xx(1,true)">
      <template v-if="a[1]">x</template>
      <template v-else></template>
    </div>
    <div class="cell" v-on:click="xx(2,true)">
      <template v-if="a[2]">x</template>
      <template v-else></template>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  name: "app",
  data() {
    return {
      a: [false,false,false]
    };
  },
  methods: {
    xx(indexOfItem,newValue) {
      Vue.set(this.a, indexOfItem, newValue)
    }
  }
};
</script>

<style>
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
