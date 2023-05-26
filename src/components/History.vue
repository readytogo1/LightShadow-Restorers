<template>
    <div class="all">
        <div class="control" @click="toggleShow" 
            :class="{ 
            'animated-class-right': !show && isFirstChange, 
            'animated-class-left': show && isFirstChange
            }">
            <i class="ri-arrow-right-s-line" v-if="show"></i>
            <i class="ri-arrow-left-s-line" v-else></i>
        </div>
        <transition name="changeShow">
            <div class="history-wrapper" v-if="show">
                <div class="img-list">
                    <div v-for="img in props.images" class="item">
                        <i class="ri-checkbox-circle-fill"></i>
                        <img :src="img">
                    </div>
                </div>
                <div class="progress-bar">
                    <span>{{ props.images.length }}/15</span>
                    <div class="progress">
                        <div class="inner"></div>
                    </div>
                </div>
                <button class="add-photo">
                    添加照片
                </button>
            </div>
        </transition>
    </div>
</template>


<script setup>
import { computed, onMounted, ref } from 'vue';
const props = defineProps(['images'])

const isFirstChange = ref(false);
const show = ref(true)
const width = computed(() => {
    return props.images.length / 15 * 100 + '%'
})
const toggleShow = function () {
    show.value = !show.value
    isFirstChange.value = true
}
</script>

<style scoped>
.animated-class-right {
    /* 定义动画样式 */
    animation: myAnimationRight 0.4s forwards ease-in-out;
}

.animated-class-left {
    /* 定义动画样式 */
    animation: myAnimationLeft 0.4s forwards ease-in-out;
}

@keyframes myAnimationRight {

    /* 定义动画关键帧 */
    from {
        transform: translateX(0);
    }

    to {
        transform: translateX(660%);
    }
}

@keyframes myAnimationLeft {

    /* 定义动画关键帧 */
    from {
        transform: translateX(660%);
    }

    to {
        transform: translateX(0);
    }
}


.changeShow-enter-active {
    animation: changeShow 0.4s ease-in-out;
}

.changeShow-leave-active {
    animation: changeShow 0.4s reverse ease-in-out;
}

@keyframes changeShow {
    from {
        transform: translateX(100%);
    }

    to {
        transform: translateX(0px);
    }
}

.all {
    width: 1024px;
    height: 686px;
    overflow: hidden;
    position: relative;
}
.history-wrapper {
    width: 200px;
    height: 646px;
    background-color: #2b2b2f;
    position: absolute;
    right: 0;
    top: 20px;
    border-top-right-radius: 20px;
    border-bottom-right-radius: 20px;
    display: flex;
    flex-direction: column;
    overflow: auto;
}
.control {
    position: relative;
    color: #fff;
    top: 300px;
    left: 810px;
    width: 30px;
    height: 60px;
    background-color: #2b2b2f;
    display: flex;
    align-items: center;
    border-radius: 20px;
    cursor: pointer;
    z-index: 999;
}

.history-wrapper::-webkit-scrollbar {
    width: 5px;
    /* //定义滚动条宽度 */
    height: 10px;
    /* //定义滚动条高度 */
    border-radius: 10px;
    /* //定义滚动条圆角 */
    background-color: rgba(240, 240, 240, 0.1);
    /* //定义滚动条颜色 */
}

/*定义滚动条轨道 内阴影+圆角*/
.history-wrapper::-webkit-scrollbar-track {
    box-shadow: inset 0 0 0px rgba(240, 240, 240, .5);
    /* //定义轨道阴影 */
    border-radius: 10px;
    /* //定义轨道圆角 */
    background-color: #121216;
    /* //定义轨道颜色 */
}

/*定义滑块 内阴影+圆角*/
.history-wrapper::-webkit-scrollbar-thumb {
    border-radius: 10px;
    /* //定义滑块圆角 */
    box-shadow: inset 0 0 0px rgba(240, 240, 240, .5);
    /* //定义滑块阴影 */
    background-color: #353539;
    /* //定义滑块颜色 */
}

.img-list {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.item {
    border-radius: 10px;
    overflow: hidden;
    position: relative;
    margin-top: 20px;
}

.item i {
    font-size: 20px;
    position: absolute;
    top: 10px;
    left: 10px;
    color: #fff;
    border-radius: 50%;
    z-index: 10;
}

.item img {
    width: 150px;
    border-radius: 10px;
    border: 2px solid white;
}
.history-wrapper .item:hover::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 9;
  }
.history-wrapper .item i:hover{
    font-size: 22px;
    transform: translateX(-1px) translateY(-1px);
}

.progress-bar {
    display: flex;
    align-items: center;
    justify-content: space-around;
    color: #dcdcdc;
    font-size: 12px;
    margin-top: 20px;
}

.progress-bar span {
    margin-right: -60px;
}

.progress {
    height: 5px;
    width: 90px;
    background-color: #323236;
    border-radius: 10px;
}

.inner {
    height: 5px;
    background-color: #fff;
    border-radius: 10px;
    width: v-bind(width);
}

.add-photo {
    width: 80%;
    height: 44px;
    line-height: 44px;
    font-size: 20px;
    background-color: #414144;
    color: #d8d8d8;
    border: none;
    border-radius: 20px;
    margin: 30px 10%;
    color: #fff;
}
.add-photo:hover{
    background-color: #3d3d40;
}
</style>