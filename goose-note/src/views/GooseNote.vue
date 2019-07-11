<template>
  <div>
    <el-row :gutter="12">
      <el-col :span="12">
        <TodayList></TodayList>
      </el-col>
      <el-col :span="12">
        <el-card class="box-card">
          <div>
            <el-collapse v-model="todoActiveName" accordion>
              <el-collapse-item title="要完成的事项" name="1">
                <TodoList></TodoList>
              </el-collapse-item>
              <el-collapse-item title="要补充的食物" name="2">
                <Foods></Foods>
              </el-collapse-item>
              <el-collapse-item title="要购买的产品" name="3">
                <Goods></Goods>
              </el-collapse-item>
              <el-collapse-item title="要观看的视频" name="4">
                <Videos></Videos>
              </el-collapse-item>
            </el-collapse>
          </div>
        </el-card>
        <br/>
        <el-card class="box-card">
          <div>
            <el-collapse v-model="infoActiveName" accordion>
              <el-collapse-item title="我的账号" name="1">
                <Accounts></Accounts>
              </el-collapse-item>
              <el-collapse-item title="我的银行卡" name="2">
                <Cards></Cards>
              </el-collapse-item>
            </el-collapse>
          </div>
        </el-card>
        <Info></Info>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import TodayList from "../components/TodayList";
import TodoList from "../components/TodoList";
import Foods from "../components/Foods";
import Goods from "../components/Goods";
import Videos from "../components/Videos";
import Accounts from "../components/Accounts";
import Cards from "../components/Cards";

export default {
  components: {
    TodayList,
    TodoList,
    Foods,
    Goods,
    Videos,
    Accounts,
    Cards
  },
  data() {
    return {
      todoActiveName: "1",
      infoActiveName: "1"
    };
  },
  mounted() {
  },
  methods: {
  }
};
</script>

<style scoped>

</style>