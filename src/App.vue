<template>
  <div>
    <div class="row">
      <Cell name="0" />
      <Cell name="1" />
      <Cell name="2" />
    </div>
    <div class="row">
      <Cell name="3" />
      <Cell name="4" />
      <Cell name="5" />
    </div>
    <div class="row">
      <Cell name="6" />
      <Cell name="7" />
      <Cell name="8" />
    </div>
    {{map}}
    {{result}}
  </div>
</template>

<script>
import Cell from "./Cell";
import Vue from "vue";
export default {
  name: "app",
  components: {
    Cell
  },
  data() {
    return {
      eventBus: new Vue(),
      map: [[null, null, null], [null, null, null], [null, null, null]],
      result: false
    };
  },
  provide() {
    return {
      eventBus: this.eventBus
    };
  },
  created() {
    const _this = this;
    this.eventBus.$on("update:has", function(x, y, z) {
      // y是true,即z为'x'，y：表示点击的是哪个Cell
      const map = _this.map;
      let i = parseInt(y);
      // let temp = map[Math.floor(i/3)]
      // temp[i%3] = z //这一步不能少
      // _this.$set(map,temp,z) //可以
      // 我怀疑这是Vue框架的bug
      // 假如temp是 map[1],z是×,那么map:[[],'x',[]]
      // 所以这z得是 [x],temp
      // _this.$set(map,temp,temp) //这个也可以
      // _this.$set(temp,temp[i%3],z) //这个也可以
      // 我怀疑这是Vue的容错性响应式更新
      map[Math.floor(i / 3)][i % 3] = z;
      _this.$set(map, map[2], "balabal"); //乱写的，只要触发一次set就好了
      _this.tell();
    });
  },
  methods: {
    tell() {
      const map = this.map;
      // 横向判断
      for (let i = 0; i < 3; i++) {
        if (
          map[i][0] != null &&
          map[i][0] == map[i][1] &&
          map[i][0] == map[i][2]
        ) {
          return (this.result = map[i][0]);
        }
      }
      // 纵向判断
      for (let j = 0; j < 3; j++) {
        if (
          map[0][j] != null &&
          map[0][j] == map[1][j] &&
          map[0][j] == map[2][j]
        ) {
          return (this.result = map[0][j]);
        }
      }
      // 对角线判断
      if (
        map[0][0] != null &&
        map[0][0] == map[1][1] &&
        map[0][0] == map[2][2]
      ) {
        return (this.result = map[0][0]);
      }
      if (
        map[0][2] != null &&
        map[0][2] == map[1][1] &&
        map[0][2] == map[2][0]
      ) {
        return (this.result = map[0][2]);
      }
    }
  }
};
</script>

<style>
.row {
  display: flex;
}
</style>
