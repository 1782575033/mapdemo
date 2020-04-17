<template>
  <div class="loction-cart">
    <div class="header">
      <div>
        <i class="iconfont icon-ditu"></i>
        <span>落脚点分析</span>
      </div>
      <div>
        <i class="iconfont icon-xiazai"></i>
      </div>
    </div>
    <div>
      <div v-for="(item,index) in mapdata" :key="index" class="list-item">
        <div class="list-item-left">
          <i class="iconfont icon-weizhi"></i>
          <span>{{index+1}}</span>
        </div>
        <div class="list-item-center">{{item.location}}</div>
        <div class="list-item-right">{{item.cnt}}次</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["mapdata"]
};
</script>

<style lang="less" scoped>
.loction-cart {
  position: fixed;
  top: 160px;
  width: 400px;
  height: 800px;
  background-color: #fff;
  z-index: 999;
  right: 15px;
  border-radius: 5px;
  .header {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    height: 55px;
    padding: 15px 20px;
    color: #2878d2;
    font-size: 16px;
    border-bottom: 1px solid #e5e5e5;
    i {
      font-size: 22px;
      margin-right: 5px;
      cursor: pointer;
    }
  }
  .list-item {
    display: flex;
    padding: 0 20px;
    align-items: center;
    height: 66px;
    cursor: pointer;
    &:hover {
      background-color: #d6eaff;
      color: #4c8ad8 !important;

      .list-item-left i {
        color: red;
        &::after {
          background-color: red;
        }
      }
      .list-item-right {
        color: #4c8ad8 !important;
      }
    }
  }
  .list-item .list-item-left {
    position: relative;
    display: flex;
    align-items: center;
    width: 40px;
    justify-content: center;
    i {
      position: absolute;
      font-size: 30px;
      color: #2878d2;
    }
    span {
      position: absolute;
      color: #fff;
      font-size: 14px;
    }
  }
  .list-item-left {
    i {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      &::after {
        content: " ";
        position: absolute;
        display: inline-block;
        width: 10px;
        height: 18px;
        background-color: #2878d2;
      }
    }
  }
  .list-item .list-item-center {
    flex: 1;
    text-align: left;
  }
  .list-item .list-item-right {
    width: 60px;
    font-style: italic;
    color: #b0b0b0;
  }
}
</style>