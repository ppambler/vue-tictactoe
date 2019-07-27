<template>
    <div class="cell" v-on:click="a = true">
      <template v-if="a">{{text}}</template>
      <template v-else></template>
    </div>
</template>

<script>
export default {
  name: "cell",
  data() {
    return {
      a: false,
      text: 'x'
    }
  }
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