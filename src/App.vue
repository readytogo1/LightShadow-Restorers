<template>
  <div class="top-bar">
    <TopBar></TopBar>
  </div>
  <div class="main">
    <div class="left-sider">
      <SiderBar :selected-options="selectedOptions" @paramSend="handleUpload"></SiderBar>
    </div>
    <div class="show-wrapper">
      <ImageComparison :images="imgPath" :scale="scale" @update:scale="scale = $event"
        @update:imageSize="imageSize = $event"></ImageComparison>
      <History :images="imgPathHis"></History>
    </div>
  </div>
  <div class="footer">
    <ZoomControls :scale="scale" :imageSize="imageSize" 
      @update:scale="scale = $event" 
      @send="handleUpload"></ZoomControls>
  </div>
</template>

<style scoped>
.left-sider {
  position: relative;
  width: 350px;
  height: 686px;
}

.show-wrapper {
  width: 1024px;
  /* margin: 50px auto; */
  position: relative;
  display: flex;
}

.main {
  display: flex;
}

.footer {
  width: 1440px;
  height: 80px;
}
</style>

<script setup>
import ImageComparison from './components/ImageComparison.vue';
import SiderBar from './components/sider/SiderBar.vue';
import TopBar from './components/TopBar.vue';
import History from './components/History.vue'
import ZoomControls from './components/ZoomControls.vue';
import axios from 'axios';

import { ref } from 'vue'
const imgPath = ref(["/img/1.jpg", '/img/2.jpg'])
const imgPathHis = ref(["/img/1.jpg"])
const selectedOptions = ref([0,0,0]);

const scale = ref(1)
const imageSize = ref({
  width: 0,
  height: 0,
})

const handleUpload = function() {
  console.log(selectedOptions.value);
  if(JSON.stringify(selectedOptions.value) === JSON.stringify([0, 0, 0])){
    alert('请至少选择一项进行优化！')
    return
  }
  const inputElement = document.createElement('input');
  inputElement.type = 'file';
  inputElement.accept = 'image/*';
  inputElement.addEventListener('change', (event) => {
      const file = event.target.files[0];
      const formData = new FormData();
      formData.append('image', file);

      // 显示加载中的界面
      showLoading();

      // 使用axios或其他网络请求库发送formData到服务器
      // 示例使用axios发送POST请求
      axios.post('http://localhost:3000/upload', formData, {
        params:selectedOptions.value
      }).then(response => {
          // 隐藏加载中的界面
          hideLoading();

          // 上传成功的处理逻辑
          imgPath.value = response.data
          imgPathHis.value = response.data.slice(0,1)
          console.log('Upload successful');
          console.log(response);
        })
        .catch(error => {
          // 隐藏加载中的界面
          hideLoading();
          // 上传失败的处理逻辑
          console.error('Upload failed:', error);
        });
});
  inputElement.click();
  function showLoading() {
  // 创建遮罩层元素
  const overlay = document.createElement('div');
  overlay.classList.add('overlay');
  
  // 设置遮罩层样式
  overlay.style.position = 'fixed';
  overlay.style.top = '0';
  overlay.style.left = '0';
  overlay.style.width = '100%';
  overlay.style.height = '100%';
  overlay.style.backgroundColor = 'rgba(255, 255, 255, 0.5)';
  overlay.style.zIndex = '99999'; // 设置层级为9999

  // 创建加载动画元素
  const spinner = document.createElement('div');
  spinner.classList.add('spinner');

  // 设置加载动画样式
  spinner.style.position = 'absolute';
  spinner.style.top = '40%';
  spinner.style.left = '50%';
  spinner.style.transform = 'translate(-50%, -50%)';
  spinner.style.border = '16px solid #f3f3f3'; // 设置加载动画的边框样式
  spinner.style.borderTop = '16px solid #3498db'; // 设置加载动画的顶部边框样式
  spinner.style.borderRadius = '50%'; // 设置加载动画的圆角半径
  spinner.style.width = '120px'; // 设置加载动画的宽度
  spinner.style.height = '120px'; // 设置加载动画的高度
  spinner.style.animation = 'spin 2s linear infinite'; // 设置旋转动画的样式

  // 添加旋转动画的关键帧样式
  const keyframes = `@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }`;

  // 创建 <style> 元素来添加关键帧样式
  const style = document.createElement('style');
  style.innerHTML = keyframes;

  // 将 <style> 元素添加到文档头部
  document.head.appendChild(style);

  // 将加载动画元素添加到遮罩层元素中
  overlay.appendChild(spinner);

  // 将遮罩层元素添加到页面中
  document.body.appendChild(overlay);
}

function hideLoading() {
  // 获取遮罩层元素
  const overlay = document.querySelector('.overlay');

  // 移除遮罩层元素
  if (overlay) {
    document.body.removeChild(overlay);
  }
}
}
</script>