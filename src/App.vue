<template>
  <div class="top-bar">
    <TopBar></TopBar>
  </div>
  <div class="main">
    <div class="left-sider">
      <SiderBar></SiderBar>
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
      @update:imgPath="imgPath = $event"></ZoomControls>
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

import { ref, reactive, readonly } from 'vue'
const imgPath = ref(["/img/1.jpg", '/img/2.jpg'])
const imgPathHis = ["/img/1.jpg","/img/3.jpg"]

const scale = ref(1)
const imageSize = ref({
  width: 0,
  height: 0,
})
</script>