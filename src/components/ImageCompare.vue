<script>
export default {
  name: "ImageCompare",
  props: {
    images: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      offsetX: 0
    };
  },
  methods: {
    startChange(event) {
      this.offsetX = event.pageX - this.$refs.slider.offsetLeft;
      window.addEventListener("mousemove", this.moveHandler);
      window.addEventListener("mouseup", this.endChange);
    },
    endChange() {
      window.removeEventListener("mousemove", this.moveHandler);
      window.removeEventListener("mouseup", this.endChange);
    },
    /* moveHandler(e) {
      this.$refs.slider.style.left = (e.pageX - this.offsetX - 4 || 0) + "px";
      this.$refs.coverImage.style.width = (e.pageX - this.offsetX || 0) + "px";
    } */
    moveHandler(e) {
        const parentWidth = this.$refs.slider.parentElement.offsetWidth;
        const newPosition = e.pageX - this.offsetX;

        // 检查移动的位置是否超出父元素的范围
        if (newPosition >= 0 && newPosition <= parentWidth) {
            this.$refs.slider.style.left = (newPosition - 4) + "px";
            this.$refs.coverImage.style.width = newPosition + "px";
        }
    }

  }
};
</script>

<template>
  <div class="image-comparison" ref="box">
    <div class="cover-image" ref="coverImage">
        <img :src="images[0]" alt="" />
    </div>
    <div class="slider" ref="slider" @mousedown="startChange">
      <div class="before">原图</div>
      <div class="after">修复后</div>
      <div class="tag-icon">
          <i class="ri-expand-left-right-line"></i>
      </div>
    </div>
    <img class="base-image" :src="images[1]" alt="" /> 
  </div>
</template>

<style scoped>
.image-comparison {
  width: 500px;
  height: 500px;
  overflow: hidden;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;  
  margin: auto;
}
/* 用于控制用户能否选中文本 */
.image-comparison * {
  user-select: none;
}
.image-comparison .slider {
  position: absolute;
  left: calc(50% - 3px);
  width: 6px;
  height: 100%;
  cursor: ew-resize;
  z-index: 20;
  background: rgba(255,255,255, 0.6);
}
.slider .before,
.after{
  width: 80px;
  height: 30px;
  line-height: 30px;
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  top: 7%;
  left: -90px;
  font-size: 20px;
  text-align: center;
  border-radius: 99px;
  cursor: default;
  color: #fff;
}
.after{
  left: 16px;
}
.image-comparison .slider .tag-icon{
  position: absolute;
  top: 75%;
  left: 50%;
  border: 1px solid rgba(0, 0, 0, 0.1);
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.9);
  transform: translate(-50%, -50%);
  display: flex;
  align-items: center;
  justify-content: center;
}
.image-comparison .slider .tag-icon i{
    font-size: 24px;
    color: rgba(0, 0, 0, 0.9);
}
.image-comparison .cover-image,
.image-comparison .base-image {
  position: absolute;
  left: 0;
  height: 100%;
  overflow: hidden;
}
.image-comparison .cover-image {
  left: 0;
  width: 50%;
  z-index: 20;
}
.image-comparison img {
  max-height: 100%;
}
</style>