<template>
  <div>
    <el-form ref="form" :model="cardsForm" label-width="80px" size="mini">
      <el-col :span="24">
        <el-form-item label="卡号">
          <el-input v-model="cardsForm.num"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item label="所属银行">
          <el-select v-model="cardsForm.source" filterable>
            <el-option
              v-for="item in cardsForm.sourceOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="卡片类型">
          <el-radio-group v-model="cardsForm.type">
            <el-radio-button label="信用卡">信用卡</el-radio-button>
            <el-radio-button label="储蓄卡">储蓄卡</el-radio-button>
          </el-radio-group>
        </el-form-item>
      </el-col>
      <el-col :span="4">
        <el-form-item>
          <el-button type="primary" @click="addCards" class="submit-btn">添加</el-button>
        </el-form-item>
      </el-col>
    </el-form>

    <el-table stripe :data="cardsList" style="width: 100%">
      <el-table-column prop="num" label="卡号"></el-table-column>
      <el-table-column prop="source" label="所属银行"></el-table-column>
      <el-table-column prop="type" label="卡片类型"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: 'Cards',
  data() {
    return {
      cardsForm: {
        num: "",
        source: '招商银行',
        sourceOptions: [
          {
            value: '招商银行',
            label: "招商银行"
          },
          {
            value: '中国工商银行',
            label: "中国工商银行"
          },
          {
            value: '中国农业银行',
            label: "中国农业银行"
          },
          {
            value: '中国建设银行',
            label: "中国建设银行"
          },
          {
            value: '中国银行',
            label: "中国银行"
          },
          {
            value: '交通银行',
            label: "交通银行"
          },
          {
            value: '中国人民银行',
            label: "中国人民银行"
          },
          {
            value: '中国民生银行',
            label: "中国民生银行"
          },
          {
            value: '中国光大银行',
            label: "中国光大银行"
          },
          {
            value: '中信银行',
            label: "中信银行"
          },
          {
            value: '上海浦东发展银行',
            label: "上海浦东发展银行"
          },
          {
            value: '兴业银行',
            label: "兴业银行"
          },
          {
            value: '华夏银行',
            label: "华夏银行"
          },
          {
            value: '中国邮政储蓄银行',
            label: "中国邮政储蓄银行"
          },
        ],
        type: "信用卡",
      },
      cardsList: [],
    };
  },
  mounted() {
    this.loadStorage();
  },
  methods: {
    loadStorage() {
      if (localStorage.getItem("cardsList")) {
        this.cardsList = JSON.parse(localStorage.getItem("cardsList"));
      }
    },
    addCards() {
      let newDate = new Date();
      let tempObj = {};
      tempObj.id = newDate.getTime();
      tempObj.num = this.cardsForm.num;
      tempObj.source = this.cardsForm.source;
      tempObj.type = this.cardsForm.type;
      this.cardsList.push(tempObj);
      localStorage.setItem("cardsList", JSON.stringify(this.cardsList));
      this.cardsForm.num = "";
      this.cardsForm.source = "招商银行";
      this.cardsForm.type = "信用卡";
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
