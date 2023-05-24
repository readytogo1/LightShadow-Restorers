<!-- <template>
<div class="slider-container">
    <input type="range" min="0.1" max="2.5" step="0.1" :value="scale" class="slider" @input="handleScaleInput">
    <span>当前尺寸：{{ imageSize.width }}px × {{ imageSize.height }}px，缩放比例：{{ (scale * 100).toFixed(0) }}%</span>
</div>
</template>

<script>
export default {
props: {
    scale: {
    type: Number,
    required: true,
    },
    imageSize: {
    type: Object,
    required: true,
    },
},
methods: {
    handleScaleInput(event) {
    const newScale = parseFloat(event.target.value);
    this.$emit('update:scale', newScale);
    },
},
};
</script>

<style scoped>
*{
color: white;
}
.slider-container {
display: flex;
align-items: center;
}

.slider {
flex-grow: 1;
}

span {
margin-left: 10px;
}
</style>
-->
<template>
    <div class="footer-container">
        <div class="slider-container">

            <span class="key">宽度：</span>
            <span class="value">{{ imageSize.width }}px</span>
            <span class="key">高度：</span>
            <span class="value">{{ imageSize.height }}px</span>
            <span class="percent value">{{ (scale * 100).toFixed(0) }}%</span>

            <i class="ri-subtract-line" @click="decreaseScale"></i>
            <input type="range" min="0.1" max="2.5" step="0.1" :value="scale" class="slider" @input="handleScaleInput">
            <i class="ri-add-line" @click="increaseScale"></i>


            <i class="ri-fullscreen-fill resize" @click="resetScale"></i>
        </div>
        <div class="upload-wrapper">
            <span>上传图片</span>
            <div>
                <i class="ri-upload-2-line"></i>
            </div>
        </div>
    </div>
</template>

<style scoped>
.footer-container{
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.slider-container .key {
    color: #666;
    font-size: 18px;
    font-weight: bold;
}

.slider-container .value {
    color: #fff;
    margin-right: 20px;
    font-weight: bold;
}

.slider-container .percent {
    width: 60px;
    margin-left: 180px;
}

.slider-container {
    margin: 0 50px;
    display: flex;
    align-items: center;
}

.slider-container i {
    font-size: 26px;
    margin: 0 5px;
    cursor: pointer;
    color: #fff;
}

.slider-container .resize {
    font-size: 24px;
    margin-left: 24px;
}


.slider {
    flex-grow: 0.01;
    width: 200px;
    -webkit-appearance: none;
    appearance: none;
    background-color: #ddd;
    height: 4px;
    border-radius: 2px;
    outline: none;
}

.slider::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 14px;
    height: 14px;
    background-color: #fff;
    border: 2px solid #ddd;
    border-radius: 50%;
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.2);
    cursor: pointer;
}

.slider::-webkit-slider-runnable-track {
    background-color: var(--inactive-color);
    /* 设置滑块左侧进度条的颜色 */
}
span{
    margin-left: 10px;
}
.upload-wrapper{
    color: #fff;
    margin-right: 80px;
    font-size: 18px;
    display: flex;
    align-items: center;
    cursor: pointer;
}
.upload-wrapper div{
    background-color: #51cef5;
    width: 40px ;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 5px;
    margin-left: 10px;
}

</style>


<script>
export default {
    props: {
        scale: {
            type: Number,
            required: true,
        },
        imageSize: {
            type: Object,
            required: true,
        },
    },
    methods: {
        handleScaleInput(event) {
            const newScale = parseFloat(event.target.value);
            this.$emit('update:scale', newScale);
        },
        decreaseScale() {
            const newScale = Math.max(this.scale - 0.1, 0.1);
            this.$emit('update:scale', newScale);
        },

        increaseScale() {
            const newScale = Math.min(this.scale + 0.1, 2.5);
            this.$emit('update:scale', newScale);
        },
        resetScale() {
            this.$emit('update:scale', 1);
        },
    },
};
</script>
