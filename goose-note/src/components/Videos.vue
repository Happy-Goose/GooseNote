<template>
  <div>
    <el-form ref="form" :model="videosForm" label-width="80px" size="mini">
      <el-col :span="24">
        <el-form-item label="名称">
          <el-input v-model="videosForm.name"></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="播放源">
          <el-select v-model="videosForm.source">
            <el-option
              v-for="item in videosForm.sourceOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </el-form-item>
      </el-col>
      <el-col :span="12">
        <el-form-item label="已看集数">
          <el-input-number v-model="videosForm.alreadyWatch" @change="handleAlreadyWatch" controls-position="right" :min="1"></el-input-number>
        </el-form-item>
      </el-col>
      <el-col :span="16">
        <el-form-item label="总集数">
          <el-slider v-model="videosForm.totalEpisode" :min="1"></el-slider>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item>
          <el-button type="primary" @click="addTowatchList" class="submit-btn">添加</el-button>
        </el-form-item>
      </el-col>
    </el-form>

    <el-table :data="towatchList" border style="width: 100%">
      <el-table-column prop="name" label="名称"></el-table-column>
      <el-table-column prop="source" label="播放源"></el-table-column>
      <el-table-column label="进度">
        <template slot-scope="scope">
          <el-progress :text-inside="true" :stroke-width="15" :percentage="scope.row.progress"></el-progress>
        </template>
      </el-table-column>
      <el-table-column label="操作" width="50">
        <template slot-scope="scope">
          <el-button @click="finishTowatch(scope.row.id)" type="text" size="small">完成</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "Videos",
  data() {
    return {
      videosForm: {
        name: "",
        source: '优酷',
        sourceOptions: [
          {
            value: '优酷',
            label: "优酷"
          },
          {
            value: '腾讯',
            label: "腾讯"
          },
          {
            value: '爱奇艺',
            label: "爱奇艺"
          },
          {
            value: 'B站',
            label: "B站"
          },
          {
            value: '人人影视',
            label: "人人影视"
          },
          {
            value: '需要下载',
            label: "需要下载"
          }
        ],
        alreadyWatch: 1,
        totalEpisode: 1
      },
      towatchList: []
    };
  },
  mounted() {
    this.loadStorage();
  },
  methods: {
    loadStorage() {
      if (localStorage.getItem("towatchList")) {
        this.towatchList = JSON.parse(localStorage.getItem("towatchList"));
      }
    },
    addTowatchList() {
      let newDate = new Date();
      let tempObj = {};
      tempObj.id = newDate.getTime();
      tempObj.name = this.videosForm.name;
      tempObj.source = this.videosForm.source;
      tempObj.progress = parseInt(this.videosForm.alreadyWatch*100/this.videosForm.totalEpisode);
      this.towatchList.push(tempObj);
      localStorage.setItem("towatchList", JSON.stringify(this.towatchList));
      this.videosForm.name = "";
      this.videosForm.source = "优酷";
      this.videosForm.alreadyWatch = 1;
      this.videosForm.totalEpisode = 1;
    },
    finishTowatch(id) {
      this.towatchList.splice(
        this.towatchList.findIndex(item => item.id === id),
        1
      );
      localStorage.setItem("towatchList", JSON.stringify(this.towatchList));
    },
    handleAlreadyWatch(value) {
      console.log(value);
      this.videosForm.totalEpisode = value;
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
.el-input-number--mini,
.el-select {
      width: 100%!important;
}
</style>
