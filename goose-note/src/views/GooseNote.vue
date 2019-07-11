<template>
  <div>
    <el-row :gutter="12">
      <el-col :span="12" :offset="2">
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
            <!-- <el-time-picker
              v-model="remindTime"
              placeholder="滚动选择提醒您此项任务的时间">
            </el-time-picker>
            <el-button type="primary">添加</el-button> -->
          </div>
          <div>
            <el-table :data="todayList" style="width: 100%">
              <el-table-column prop="content" label="内容"></el-table-column>
              <el-table-column label="操作" width="150">
                <template slot-scope="scope">
                  <el-button @click="finish(scope.row.id)" type="text" size="small">完成</el-button>
                  <el-button type="text" size="small">推迟</el-button>
                  <el-button type="text" size="small">提醒</el-button>
                </template>
              </el-table-column>
            </el-table>
          </div>
        </el-card>
      </el-col>
      <el-col :span="8">
        <el-card class="box-card">
          <div slot="header">
            <span>待办</span>
          </div>
          <div>
            <el-collapse v-model="todoActiveName" accordion>
              <el-collapse-item title="要完成的事项" name="1">
                <el-input
                  v-model="todoContentInput"
                  placeholder="输入你要完成的事项,回车结束"
                  @keyup.enter.native="addTodoList"
                ></el-input>
                <el-table :data="todoList" style="width: 100%">
                  <el-table-column prop="content" label="内容"></el-table-column>
                  <el-table-column label="操作" width="50">
                    <template slot-scope="scope">
                      <el-button @click="finishTodo(scope.row.id)" type="text" size="small">完成</el-button>
                    </template>
                  </el-table-column>
                </el-table>
              </el-collapse-item>
              <el-collapse-item title="要补充的食物" name="2">
                <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
              </el-collapse-item>
              <el-collapse-item title="要购买的产品" name="3">
                <div>帮助用户识别：界面简单直白，让用户快速识别而非回忆，减少用户记忆负担。</div>
              </el-collapse-item>
              <el-collapse-item title="要观看的视频" name="4">
                <div>用户决策：根据场景可给予用户操作建议或安全提示，但不能代替用户进行决策；</div>
              </el-collapse-item>
            </el-collapse>
          </div>
        </el-card>
        <br/>
        <el-card class="box-card">
          <div slot="header">
            <span>信息</span>
          </div>
          <div>
            <el-collapse v-model="infoActiveName" accordion>
              <el-collapse-item title="我的账号" name="1">
                <div>与现实生活一致：与现实生活的流程、逻辑保持一致，遵循用户习惯的语言和概念；</div>
              </el-collapse-item>
              <el-collapse-item title="我的银行卡" name="2">
                <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
              </el-collapse-item>
              <el-collapse-item title="我的灵感" name="3">
                <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
              </el-collapse-item>
            </el-collapse>
          </div>
        </el-card>

      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      todayContentInput: "",
      todayList: [],
      todoContentInput: "",
      todoList: [],
      remindTime: "",
      todoActiveName: "1",
      infoActiveName: "1"
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
      if (localStorage.getItem("todoList")) {
        this.todoList = JSON.parse(localStorage.getItem("todoList"));
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
    addTodoList() {
      let newDate = new Date();
      let tempObj = {};
      tempObj.id = newDate.getTime();
      tempObj.content = this.todoContentInput;
      this.todoList.push(tempObj);
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
      this.todoContentInput = "";
    },
    finishToday(id) {
      console.log(id);
    },
    finishTodo(id) {
      console.log(id);
    }
  }
};
</script>

<style scoped>
.box-card {
  width: 100%;
}
</style>