<script setup>

</script>

<template>
    <div class="bar-wrapper">
        <div class="brand-wrapper">
            <a href="/" class="brand">
                <img src="/static/logo.png" alt="">
            </a>
        </div>
        <div class="operation-wrapper">
            <span class="help op">帮助</span>
            <button class="log-reg op">登录 / 注册</button>
            <div class="line"></div>
            <button class="download op">下载
                <i class="ri-download-line"></i>
            </button>
        </div>
    </div>
</template>

<style scoped>
    .bar-wrapper{
        width: 1440px;
        height: 74px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .brand-wrapper{
        margin-left: 50px;
    }
    .brand img{
        height: 40px;
        line-height: 40px;
    }
    .operation-wrapper{
        display: flex;
        align-items: center;
        margin-right: 50px;
    }
    .line{
        width: 1px;
        height: 24px;
        background-color: rgba(255, 255, 255, .2);
        margin: 0 30px;
    }
    .operation-wrapper .op {
        border-radius: 200px;
        font-size: 20px;
        height: 40px;
        line-height: 40px;
        text-align: center;
        margin: 0 10px;
        vertical-align: middle;
    }
    .operation-wrapper .op:hover {
        cursor: pointer;
    }
    .help{
        color: white;
        width: 100px;
    }
    .log-reg{
        width: 150px;
        border: 2px solid rgba(255, 255, 255, .15);
        background-color: rgba(255, 255, 255, 0);
        color: #fff;
    }
    .download{
        width: 120px;
        background-color: #51cef5;
        border-color: rgba(255, 255, 255, .15);
        color: #fff;
    }
</style>