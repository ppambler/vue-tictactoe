<template>
  <div>
    <div class="row">
      <Cell name="cell1"/>
      <Cell name="cell2"/>
      <Cell name="cell3"/>
    </div>
    <div class="row">
      <Cell name="cell4"/>
      <Cell name="cell5"/>
      <Cell name="cell6"/>
    </div>
    <div class="row">
      <Cell name="cell7"/>
      <Cell name="cell8"/>
      <Cell name="cell9"/>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell";
import Vue from "vue"
export default {
  name: "app",
  components: {
    Cell
  },
  data() {
    return {
      eventBus: new Vue(),
    }
  },
  provide() {
    return {
      eventBus: this.eventBus
    }
  },
  created() {
    this.eventBus.$on('update:has',function(x) {
      // console.log('你有拿到值吗？')
    })
  },
};
</script>

<style>
  .row {
    display: flex;
  }
</style>
