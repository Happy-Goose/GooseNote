<template>
  <div>
    <el-form ref="form" :model="accountForm" label-width="120px" size="mini">
      <el-col :span="24">
        <el-form-item label="登录设备/网站">
          <el-input v-model="accountForm.url"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="16">
        <el-form-item label="账号">
          <el-input v-model="accountForm.account"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item>
          <el-button type="primary" @click="addAccounts" class="submit-btn">添加</el-button>
        </el-form-item>
      </el-col>
    </el-form>

    <el-table stripe :data="accountsList" style="width: 100%">
      <el-table-column prop="url" label="登录设备/网站"></el-table-column>
      <el-table-column prop="account" label="账号"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'Accounts',
  data() {
    return {
      accountForm: {
        url: "",
        account: "",
      },
      accountsList: []
    };
  },
  mounted() {
    this.loadStorage();
  },
  methods: {
    loadStorage() {
      if (localStorage.getItem("accountsList")) {
        this.accountsList = JSON.parse(localStorage.getItem("accountsList"));
      }
    },
    addAccounts() {
      let newDate = new Date();
      let tempObj = {};
      tempObj.id = newDate.getTime();
      tempObj.url = this.accountForm.url;
      tempObj.account = this.accountForm.account;
      this.accountsList.push(tempObj);
      localStorage.setItem("accountsList", JSON.stringify(this.accountsList));
      this.goodsForm.url = "";
      this.goodsForm.account = 1;
    },
  }
}
</script>

<style scoped lang="scss">
.box-card {
  width: 100%;
}
.submit-btn {
  float: right;
}
</style>
