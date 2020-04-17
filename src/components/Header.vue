<template>
  <div class="header">
    <div class="logo">Logo</div>
    <div class="center-option">
      <div
        :class="['center-option-item',{ active: item.active }]"
        v-for="item in options"
        :key="item.id"
        @click="check(item.id)"
      >
        <i :class="[item.icon]"></i>
        {{item.name}}
      </div>
    </div>
    <div class="person-option">
      <div class="msg">
        <i class="iconfont icon-xiaoxi"></i>
        <div class="tip">2</div>
      </div>
      <div class="warn">
        <i class="iconfont icon-xiaoxi1"></i>
        <div class="tip">99+</div>
      </div>
      <div class="user-info">
        欢迎您！Admin
        <i class="iconfont icon-guanji"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: [
        {
          id: 1,
          name: "目标管理",
          active: true,
          icon: "iconfont icon-renyuan"
        },
        {
          id: 2,
          name: "告警中心",
          active: false,
          icon: "iconfont icon-xiaoxi1"
        },
        {
          id: 3,
          name: "系统管理",
          active: false,
          icon: "iconfont icon-shezhi"
        }
      ]
    };
  },
  methods: {
    check(id) {
      this.options.forEach(item => {
        if (item.id == id) {
          item.active = true;
          return true;
        } else {
          item.active = false;
        }
      });
    }
  }
};
</script>

<style lang="less" scoped>
.header {
  z-index: 999;
  height: 66px;
  background-color: #2881d2;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  .logo {
    margin-left: 20px;
    font-size: 25px;
    font-weight: bold;
    color: #fff;
    text-transform: uppercase;
    width: 30%;
    display: flex;
    justify-content: flex-start;
  }
  .center-option {
    display: flex;
    font-size: 14px;
    justify-content: center;
    align-items: center;
    width: 40%;
    .center-option-item {
      margin: 0 25px;
      color: #72a6d2;
      cursor: pointer;
      &.active {
        color: #fff;
      }
    }
  }
  .person-option {
    display: flex;
    align-items: center;
    width: 30%;
    display: flex;
    justify-content: flex-end;
    .msg {
      width: 40px;
      height: 40px;
      background-color: #036dc1;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      cursor: pointer;

      position: relative;
      margin-right: 50px;
      i {
        font-size: 20px;
      }
    }
    .warn {
      width: 40px;
      height: 40px;
      background-color: #036dc1;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      margin-right: 70px;

      position: relative;
      cursor: pointer;
      i {
        font-size: 20px;
      }
    }
    .user-info {
      color: #fff;
      i {
        margin: 0 5px;
        font-size: 18px;
      }
    }
  }
  .tip {
    position: absolute;
    height: 15px;
    padding: 1px 6px;
    top: 2px;
    left: 30px;
    border-radius: 7.5px;
    background-color: red;
    font-size: 12px;
  }
}
</style>