<template>
  <div>
    <el-form ref="form" :model="goodsForm" label-width="80px" size="mini">
      <el-col :span="24">
        <el-form-item label="名称">
          <el-input v-model="goodsForm.name"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item label="数量">
          <el-input-number v-model="goodsForm.num" :min="1"></el-input-number>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item label="金额">
          <el-input v-model="goodsForm.money"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item>
          <el-button type="primary" @click="addGoods" class="submit-btn">添加</el-button>
        </el-form-item>
      </el-col>
    </el-form>

    <el-table :data="tobuyList" border show-summary style="width: 100%">
      <el-table-column prop="name" label="名称"></el-table-column>
      <el-table-column prop="num" sortable label="数量"></el-table-column>
      <el-table-column prop="money" sortable label="金额"></el-table-column>
      <el-table-column label="操作" width="50">
        <template slot-scope="scope">
          <el-button @click="finishTobuy(scope.row.id)" type="text" size="small">完成</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "Goods",
  data() {
    return {
      goodsForm: {
        name: "",
        num: 1,
        money: 100
      },
      tobuyList: []
    };
  },
  mounted() {
    this.loadStorage();
  },
  methods: {
    loadStorage() {
      if (localStorage.getItem("tobuyList")) {
        this.tobuyList = JSON.parse(localStorage.getItem("tobuyList"));
      }
    },
    addGoods() {
      let newDate = new Date();
      let tempObj = {};
      tempObj.id = newDate.getTime();
      tempObj.name = this.goodsForm.name;
      tempObj.num = this.goodsForm.num;
      tempObj.money = this.goodsForm.money;
      this.tobuyList.push(tempObj);
      localStorage.setItem("tobuyList", JSON.stringify(this.tobuyList));
      this.goodsForm.name = "";
      this.goodsForm.num = 1;
      this.goodsForm.money = 100;
    },
    finishTobuy(id) {
      this.tobuyList.splice(
        this.tobuyList.findIndex(item => item.id === id),
        1
      );
      localStorage.setItem("tobuyList", JSON.stringify(this.tobuyList));
    }
  }
};
</script>

<style scoped lang="scss">
.box-card {
  width: 100%;
}
.submit-btn {
  float: right;
}
</style>
