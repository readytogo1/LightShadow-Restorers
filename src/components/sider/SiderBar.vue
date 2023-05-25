<script setup>
import ModelOpt from './ModelOpt.vue';
</script>

<template>
    <div class="side-wrapper">
        <div class="tool-title">工具栏</div>
        <ModelOpt title="图像增强" description="提升图像细节" logoIcon="ri-image-line" logoColor="#f8df72"
        :options="['基础版', 'v1版']" />
        <ModelOpt title="图像修复" description="修复图像空缺裂痕" logoIcon="ri-tools-line" logoColor="#77b483"
        :options="['基础版', 'v1版']" />
        <ModelOpt title="图像上色" description="为图像增添色彩" logoIcon="ri-palette-fill" logoColor="#ffbfc8"
            :options="['不使用', '基础版']" />
        <button class="apply-btn">应用</button>
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
}

::-webkit-scrollbar {
    display: none;
}

.tool-title {
    color: #b1b1b8;
    margin-bottom: 20px;
    font-size: 19px;
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
    margin-top: 20px;
}
</style>