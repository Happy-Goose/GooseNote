<template>
  <div>
    <el-input
      v-model="todoContentInput"
      placeholder="输入你要完成的事项,回车结束"
      @keyup.enter.native="addTodoList"
    ></el-input>
    <el-table stripe :data="todoList" style="width: 100%">
      <el-table-column prop="content" label="内容"></el-table-column>
      <el-table-column label="操作" width="50">
        <template slot-scope="scope">
          <el-button @click="finishTodo(scope.row.id)" type="text" size="small">完成</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      todoActiveName: "1",
      todoContentInput: "",
      todoList: [],
    };
  },
  mounted() {
    this.loadStorage();
  },
  methods: {
    loadStorage() {
      if (localStorage.getItem("todoList")) {
        this.todoList = JSON.parse(localStorage.getItem("todoList"));
      }
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
    finishTodo(id) {
      this.todoList.splice(
        this.todoList.findIndex(item => item.id === id),
        1
      );
      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    }
  }
}
</script>

<style scoped lang="scss">
</style>
