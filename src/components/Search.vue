<template>
  <div class="search">
    <div class="lable">
      <i class="iconfont icon-ditu"></i>
      <span>落脚点分析</span>
    </div>
    <div class="search-fac">
      <div class="lable">查询条件：</div>
      <el-select v-model="value" placeholder="请选择" popper-class="seleteA" @change="change">
        <el-option
          v-for="item in userdata"
          :key="item.value"
          :label="item.label"
          :value="item.targetName + '--' + item.phoneNumber + '--' + item.imsi"
        ></el-option>
      </el-select>
    </div>
    <div class="search-time">
      <div class="lable">时间范围：</div>
      <el-date-picker
        v-model="dateStart"
        type="datetime"
        placeholder="选择日期时间"
        prefix-icon="iconfont icon-icon-"
      ></el-date-picker>
      <div class="lable-bt">--</div>
      <el-date-picker
        v-model="dateEnd"
        type="datetime"
        placeholder="选择日期时间"
        prefix-icon="iconfont icon-icon-"
      ></el-date-picker>
    </div>
    <div class="search-btn">
      <el-button type="primary" icon="el-icon-search" @click="search">搜索</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      dateStart: "",
      dateEnd: ""
    };
  },
  props: ["userdata"],
  methods: {
    change(e) {
      console.log(e);
    },
    search() {
      this.$emit("search");
    }
  },

  mounted() {
    console.log(this.userdata);
  }
};
</script>

<style lang="less" scoped>
.search {
  position: fixed;
  top: 90px;
  z-index: 999;
  margin: 0 15px;
  background-color: #fff;
  height: 50px;
  width: calc(100% - 30px);
  border-radius: 5px;
  box-shadow: 0 0 1px #000 inset;
  display: flex;
  align-items: center;
  padding: 0 20px;
  .lable {
    display: flex;
    align-items: center;
    color: #2f7cd3;
    i {
      font-size: 20px;
    }
    span {
      font-size: 16px;
      font-weight: bold;
      margin-left: 5px;
    }
  }
  .search-fac {
    display: flex;
    align-items: center;
    margin-left: 40px;
    .lable {
      font-size: 14px;
      color: black;
    }
    .seleteA {
      height: 32px !important;
    }
  }
  .search-time {
    margin-left: 40px;
    display: flex;
    align-items: center;
    .lable {
      font-size: 14px;
      color: black;
    }
    .lable-bt {
      margin: 0 5px;
    }
  }
  .search-btn {
    margin-left: 20px;
  }
}
</style>