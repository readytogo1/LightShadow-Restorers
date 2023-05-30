<script setup>
import ModelOpt from './ModelOpt.vue';
import {ref} from "vue"
const selectedOptions = ref([0,0,0]);

function handleOptionSelected(index, selected) {
  selectedOptions.value[index] = selected;
}
function handleApply() {
  // 对每个子组件的选中索引进行处理
  selectedOptions.value.forEach((selected, index) => {
    console.log(`子组件 ${index} 的选中索引：`, selected);
    // 在这里可以执行根据选中索引进行的后续处理操作
  });
}
</script>

<template>
    <div class="side-wrapper">
        <div class="tool-title">工具栏</div>
        <ModelOpt title="图像增强" description="提升图像细节" logoIcon="ri-image-line" logoColor="#f8df72"
        :options="['不使用', 'v1版']" @selected="handleOptionSelected(0, $event)"/>
        <ModelOpt title="图像修复" description="修复图像空缺裂痕" logoIcon="ri-tools-line" logoColor="#77b483"
        :options="['不使用', 'v1版']" @selected="handleOptionSelected(1, $event)"/>
        <ModelOpt title="图像上色" description="为图像增添色彩" logoIcon="ri-palette-fill" logoColor="#ffbfc8"
            :options="['不使用', '柔和', '冷色调']" typeOpt="1" desc="自动上色" 
            :optionsImg="['/img/style_img/prohibited.png','/img/style_img/soft.png','/img/style_img/coolcolourtone.png']"
            @selected="handleOptionSelected(2, $event)"/>
    </div>
    <div class="button-wrapper">
        <button class="apply-btn" @click="handleApply">应用</button>
    </div>
</template>


<style scoped>
.side-wrapper {
    position: absolute;
    border-radius: 20px;
    background-color: #222226;
    width: 250px;
    height: 646px;
    top: 20px;
    left: 50px;
    padding: 20px;
    box-sizing: border-box;
    overflow: auto;
    padding-bottom: 70px;
}

::-webkit-scrollbar {
    display: none;
}

.tool-title {
    color: #b1b1b8;
    margin-bottom: 20px;
    font-size: 19px;
}
.button-wrapper{
    width: 210px;
    height: 90px;
    background-color: #222226;
    position: absolute;
    bottom: 20px;
    left: 70px;
}
.apply-btn {
    background-color: #51cef5;
    border-radius: 30px;
    color: white;
    width: 210px;
    height: 40px;
    border: none;
    font-size: 17px;
    line-height: 17px;
    position: absolute;
    top: 30px;
}
</style>