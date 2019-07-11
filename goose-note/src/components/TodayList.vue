<template>
  <div>
    <el-card class="box-card">
      <div slot="header">
        <span>今日待办</span>
      </div>
      <div>
        <el-input
          v-model="todayContentInput"
          placeholder="在这里添加你今天要完成的内容,按回车结束"
          @keyup.enter.native="addTodayList"
        ></el-input>
      </div>
      <div>
        <el-table :data="todayList" style="width: 100%">
          <el-table-column prop="content" label="内容"></el-table-column>
          <el-table-column label="操作" width="150">
            <template slot-scope="scope">
              <el-button @click="finishToday(scope.row.id)" type="text" size="small">完成</el-button>
              <el-button type="text" size="small">推迟</el-button>
              <el-button type="text" size="small">提醒</el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "TodayList",
  data() {
    return {
      todayContentInput: "",
      todayList: [],
      remindTime: ""
    };
  },
  mounted() {
    this.loadStorage();
  },
  methods: {
    loadStorage() {
      if (localStorage.getItem("todayList")) {
        this.todayList = JSON.parse(localStorage.getItem("todayList"));
      }
    },
    addTodayList() {
      let newDate = new Date();
      let tempObj = {};
      tempObj.id = newDate.getTime();
      tempObj.content = this.todayContentInput;
      this.todayList.push(tempObj);
      localStorage.setItem("todayList", JSON.stringify(this.todayList));
      this.todayContentInput = "";
    },
    finishToday(id) {
      this.todayList.splice(
        this.todayList.findIndex(item => item.id === id),
        1
      );
      localStorage.setItem("todayList", JSON.stringify(this.todayList));
    }
  }
};
</script>

<style scoped lang="scss">
.box-card {
  width: 100%;
}
</style>
