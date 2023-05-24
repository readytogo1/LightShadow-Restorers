<script setup>

</script>

<template>
    <div class="title-bar">
        <div class="logo">
            <i class="ri-image-line"></i>
        </div>
        <div class="title-wrapper">
            <h2 class="title">图像增强</h2>
            <span class="desc">提升图像细节</span>
        </div>
    </div>
    <div class="option-bar">
        <button class="base chosen">基础版</button>
        <button class="v1">v1版</button>
    </div>
</template>

<style scoped>
.title-bar{
    display: flex;
    align-items: center;
    margin-top: 10px;
}
.logo{
    background-color: #f8df72;
    width: 40px;
    height: 40px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 20px;
}
i{
    color: #fff;
    font-size: 32px;
}
.title-wrapper h2{
    color: #dcdcdc;
    font-size: 16px;
    margin-bottom: 2px;
}
.title-wrapper .desc{
    color: #b1b1b8;
    font-size: 15px;
}
.option-bar button{
    color: #dcdcdc;
    background-color: #000;
    border: 2px solid #353539;
    border-radius: 10px;
    font-size: 14px;
    height: 40px;
    margin: 20px 10px;
    margin-left: 0;
    padding: 5px 16px;
}
.option-bar .chosen{
    background-color: #353539;
}
.option-bar{
    border-bottom: 1px solid #2a2a2e;
    padding-bottom: 20px;
}
</style>