<template>
  <el-transfer v-model="needToBuy" :data="allFoods" :titles="['经常吃的', '需要买的']"></el-transfer>
</template>

<script>
export default {
  name: "Foods",
  data() {
    return {
      needToBuy: [],
      allFoods: [{ key: 1, label: "小米椒" }, { key: 2, label: "大蒜" }]
    };
  },
  mounted() {
  },
  methods: {
  }
};
</script>

<style lang="scss">
.el-transfer-panel__body {
  text-align: left!important;
}
.el-checkbox {
  display: block!important;
}
</style>
