<template>
  <div class="wrapper">
    <div>{{`当前为第${n}手，下一手是${play}下`}}</div>
    <div class="chessboard">
      <div class="row">
        <Cell name="0" :isOver="isOver" />
        <Cell name="1" :isOver="isOver" />
        <Cell name="2" :isOver="isOver" />
      </div>
      <div class="row">
        <Cell name="3" :isOver="isOver" />
        <Cell name="4" :isOver="isOver" />
        <Cell name="5" :isOver="isOver" />
      </div>
      <div class="row">
        <Cell name="6" :isOver="isOver" />
        <Cell name="7" :isOver="isOver" />
        <Cell name="8" :isOver="isOver" />
      </div>
    </div>
    <div>结果：{{result == null ? '胜负未分' : `胜方为${result}`}}</div>
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
      result: null,
      isOver: false,
      n: 0,
      play: '×'
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
      _this.n++;
      x ? _this.play = '○' : _this.play = '×'
      console.log(y)
      let i = parseInt(y);
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
          this.isOver = true
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
          this.isOver = true
          return (this.result = map[0][j]);
        }
      }
      // 对角线判断
      if (
        map[0][0] != null &&
        map[0][0] == map[1][1] &&
        map[0][0] == map[2][2]
      ) {
        this.isOver = true
        return (this.result = map[0][0]);
      }
      if (
        map[0][2] != null &&
        map[0][2] == map[1][1] &&
        map[0][2] == map[2][0]
      ) {
        this.isOver = true
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
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
