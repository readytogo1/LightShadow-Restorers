<script setup>
import EnhanceOpt from './EnhanceOpt.vue';
import InpaintOpt from './InpaintOpt.vue';
import ColorOpt from "./ColorOpt.vue"
</script>

<template>
    <div class="side-wrapper">
        <div class="tool-title">工具栏</div>
        <EnhanceOpt></EnhanceOpt>
        <InpaintOpt></InpaintOpt>
        <ColorOpt></ColorOpt>
        <button class="apply-btn">应用</button>
    </div>
</template>


<style scoped>

.side-wrapper{
    position: absolute;
    border-radius: 20px;
    background-color: #121216;
    width: 250px;
    height: 646px;
    top: 20px;
    left: 50px;
    padding: 20px;
    box-sizing: border-box;
    overflow: auto;
}
::-webkit-scrollbar{
    display:none;
}
.tool-title{
    color: #b1b1b8;
    margin-bottom: 20px;
    font-size: 19px;
}
.apply-btn{
    background-color: #ff3a5c;
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