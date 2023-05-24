<script setup>

</script>

<template>
    <div class="footer">
        <div class="size-wrapper">
            <p class="img-width">
                <span class="key">宽度：</span>
                <span class="value">988px</span>
            </p>
            <p class="img-height">
                <span class="key">高度：</span>
                <span class="value">1432px</span>
            </p>
        </div>
        <div class="zoom-wrapper">
            <span>10%</span>
            <div class="zoom-bar">
                <i class="ri-subtract-line"></i>
                <div class="progress">
                    <div class="inner"></div>
                </div>
                <i class="ri-add-line"></i>
            </div>
            <i class="ri-fullscreen-fill"></i>
        </div>
        <div class="upload-wrapper">
            <span>上传图片</span>
            <i class="ri-upload-2-line"></i>
        </div>
    </div>

</template>

<style scoped>
.footer{
    display: flex;
    align-items: center;
}
.size-wrapper{
    display: flex;
    margin: 50px;
    
}
.size-wrapper .key{
    color: #666;
    font-size: 18px;
    font-weight: bold;
}
.size-wrapper .value{
    color: #fff;
    margin-right: 20px;
    font-weight: bold;
}
.zoom-wrapper{
    display: flex;
}
.zoom-wrapper span{
    color: #fff;
    font-size: 18px;
    font-weight: bold;
}
.zoom-wrapper .zoom-bar{
    display: flex;
}
</style>