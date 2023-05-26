<template>
  <div>
    <!-- 其他组件内容 -->

    <Mask :is-show="isShow" @hide="$emit('hide')">
      <!-- 需要在遮罩层内显示的登录弹窗 -->
      <div class="log-layer">
        <i class="ri-close-line" @click="$emit('hide')"></i>
        <h1>登录 / 注册</h1>
        <h2>登录或创建您的帐户以访问更多增强功能</h2>
        <div class="opt-wrapper">
          <button>
            <i class="ri-wechat-fill"></i>
            <span>使用微信账号登录</span> 
          </button>
          <button>
            <i class="ri-github-fill"></i>
            <span>使用github账号登录</span> 
          </button>
          <button>
            <i class="ri-apple-fill"></i>
            <span>使用Apple账号登录</span>
          </button>
        </div>
        <p>登录，即表示您接受我们的 <a href="">服务条款</a> 并确认收到我们的 <a href="">隐私和 Cookie 政策</a> </p>
      </div>
    </Mask>
  </div>
</template>

<script setup>
import Mask from '../UI/Mask.vue'; // 导入 Mask.vue 组件
import { defineProps, defineEmits } from 'vue';

const props = defineProps(['isShow'])
const emits = defineEmits(['hide']);

</script>

<style scoped>
.log-layer{
  width: 400px;
  height: 550px;
  background-image: url('/static/bc.jpg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 64px 40px;
  margin: auto;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
}
.log-layer>i{
  color: #000;
  font-size: 30px;
  position: absolute;
  top: 10px;
  left: 10px;
  cursor: pointer;
}
h1{
  font-size: 24px;
}
h2{
  color: #646466;
  margin-top: 10px;
  margin-bottom: 10px;
  font-size: 18px;
}

.opt-wrapper{
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}
.opt-wrapper button{
  width: 300px;
  height: 50px;
  background-color: #fff;
  border-radius: 99px;
  border: 2px solid black;
  margin: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.opt-wrapper button i{
  font-size: 24px;
  margin-right: 10px;
}
.opt-wrapper button span{
  font-size: 14px;
}
</style>