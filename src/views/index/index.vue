<template>
  <!-- 样式在app.vue中 -->
  <div class="wrapper-inner" id="app">
    <!-- 返回顶部 -->
    <div id="dtop" class="gotop" title="返回顶部" @click="movetop">
      <svg class="icon" aria-hidden="true">
        <use xlink:href="#icon-ico-top"></use>
      </svg>
      <div class="bg"></div>
      <div class="circle"></div>
    </div>
    <div class="main" type="flex">
      <div class="main-left" :class="{'container-left-width':this.$store.state.isLeftHiden}">
        <me-nu></me-nu>
      </div>
      <head-banner></head-banner>
      <div class="main-right" :class="{'container-width':this.$store.state.isLeftHiden}">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
// 格式要特别注意字母大小写
import meNu from "../../components/menu";
import headBanner from "../../components/headBanner";
export default {
  data() {
    return {
      userName: ""
    };
  },
  mounted() {
    // this.getName();
    // this.tologin();//判断是否登陆
    window.addEventListener("scroll", this.returntop, true); // 监听（绑定）滚轮滚动事件
  },
  methods: {
    tologin() {
      if (this.userName == "" || this.userName == null) {
        this.$message.error("请进行登录!");
        console.log(this.userName);
        this.$router.push("/login");
      }
    },
    //返回顶部
    returntop() {
      //返回顶部
      var htop = document.documentElement.scrollTop; //获取滚动高度
      //判断滚动条滚动长度
      // if (htop > 350) {
      //   $(".gotop")
      //     .stop()
      //     .fadeIn();
      // } else {
      //   $(".gotop")
      //     .stop()
      //     .fadeOut();
      // }
    },
    movetop() {
      // $("body,html").animate({ scrollTop: 0 }, 300);
    },
    openCenter() {
      if (this.userName == "admin") {
        this.$message({
          dangerouslyUseHTMLString: true, //表示提示的是html片段
          message:
            '<svg class="icon" aria-hidden="true"> <use xlink:href="#icon-jiqiren"></use> </svg> ' +
            "欢迎登陆您民盛报送系统！",
          type: "success",
          center: true
        });
      } else {
        this.$message({
          dangerouslyUseHTMLString: true,
          message:
            '<svg class="icon" aria-hidden="true"> <use xlink:href="#icon-shengqi"></use> </svg> ' +
            "请先登录！",
          type: "warning",
          center: true
        });
      }
    },

    //获取用户名，vue 本地存储数据 sessionStorage
    getName() {
      let userName = sessionStorage.getItem("username");
      this.userName = userName;
    }
  },
  watch: {},
  components: {
    meNu,
    headBanner
  }
};
</script>

<style lang='less'>
.top {
  width: 100%;
  height: 50px;
}

//整个大页面
.main {
  width: 100%;
  display: flex;
  .main-left {
    position: fixed;
    flex-shrink: 1;
    width: 12%;
    height: 100%;
    transition: all 0.5s;
    z-index: 100;
  }
  .main-right {
    flex-shrink: 0;
    width: 88%;
    float: right;
    transition: all 0.5s;
    margin-left: 12%;
  }
}

// 右半部分扩张
.container-width {
  transition: all 0.5s;
  width: 96% !important;
  margin-left: 4% !important;
}
.container-left-width {
  transition: all 0.5s;
  width: 4% !important;
}
.wrapper-inner {
  width: 100%;
  height: 0;
  padding-bottom: 70%;

  background: rgb(238, 237, 237);
}

.icon {
  overflow: hidden;
  width: 3.1em;
  height: 3.1em;
  vertical-align: -0.9em;
  fill: currentColor;
  padding: 3px 5px;
}
</style>
