<template>
  <div class="container">
    <div class="userinfo" @click="bindViewTap">
      <open-data type="userAvatarUrl"></open-data>
      <div class="userinfo-nickname">
        <!-- <open-data type="groupName" open-gid="xxxxxx"></open-data> -->
      </div>
    </div>
    <mp-button @click="testHandle" type="primary" size="large" btnClass="mb15">确定/取消111</mp-button>
    <mp-button @click="testHandle1" type="primary" size="large" btnClass="mb15">提示窗口111</mp-button>
     <div open-type="contact"  >客服</div>
    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>
    <form class="form-container">
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>
    <a href="/pages/index1/main" class="counter">index</a>
    <a href="/pages/counter/main" class="counter">去往Vuex示例页面</a>
    <a href="/pages/activity/main" class="counter">去往活动页面</a>
    <a href="/pages/appointment/main" class="counter">去往预约页面</a>
    <a href="/pages/appointmentComplete/main" class="counter">去往预约成功页面</a>
    <a href="/pages/cascadeFlow/main" class="counter">去往瀑布流页面</a>
    <a href="/pages/designerList/main" class="counter">去往设计师列表页面</a>
    <a href="/pages/downloadPic/main" class="counter">去往下载图片页面</a>
    <a href="/pages/userCenter/main" class="counter">去往用户中心页面</a>
  </div>
</template>

<script>
import card from "@/components/card";
import mpButton from "mpvue-weui/src/button";
import {get, post} from "@/http/api"
export default {
  data() {
    return {
      motto: "Hello World",
      userInfo: {}
    };
  },

  components: {
    card,
    mpButton
  },
  onShow() {
    console.log('show')
  },
  methods: {
    testHandle() {
      wx.showModal({
        //title: '弹窗标题',
        content: '请先完善您的个人信息 才可以预约摄影师',
        confirmText: "确定",
        cancelText: "取消",
        success:  (res) => {
          console.log(res);
          if (res.confirm) {
            console.log('确定')
          } else {
            console.log('取消')
          }
        }
      });
    },
    testHandle1() {
      wx.showModal({
        content: '提交成功',
        showCancel: false,
        success:  (res) => {
          if (res.confirm) {
            console.log('用户点击确定')
          }
        }
      });

    },
    bindViewTap() {
      const url = "../counter/main";
      console.log(123);
      //mpvue-router跳转
      this.$router.push({ path: url, query: {} });

      // 微信小程序原生跳转
      // wx.navigateTo({ url });
    },
    clickHandle(msg, ev) {
      console.log("clickHandle:", msg, ev);
    },

    // 调取摄影师列表
    getPhotographersList() {
      
      let params = {
        url: '/list/',
        data: {
          value: "wang"
        }
      }
      get(params).then(res=>{ 
        console.log(res) 
      })
    },

    // 创建摄影师
    createPhotographers() {
      let params = {
        url: '/list/',
        data: {
          Cameraman_style: "aaa",
          Cameraman_name: "bbb"
        }
      }
      post(params).then(res=>{ console.log(res) })
    }
  },

  
  mounted(){
  },
  created() {

  }
};
</script>

<style lang="scss" scoped>
$b2: #f4f4f4;
$b3: #ccc;
$b5: #333;
$b4: #999;
$b1: #2da4ff;
$y2: #ff7b33;
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: $b4;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 0.2rem;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
