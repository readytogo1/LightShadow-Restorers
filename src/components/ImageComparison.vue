<template>
  <div class="image-comparison" ref="box">
    <div class="cover-image" ref="coverImage">
      <Image :imageUrl="images[0]" :scale="scale" @update:imageSize="onImageSizeUpdate" @update:scale="onScaleUpdate">
      </Image>
    </div>
    <div class="slider" ref="slider" @mousedown="startChange">
      <div class="before">原图</div>
      <div class="after">修复后</div>
      <div class="tag-icon">
        <i class="ri-expand-left-right-line"></i>
      </div>
    </div>
    <Image :imageUrl="images[1]" :scale="scale" @update:imageSize="onImageSizeUpdate" @update:scale="onScaleUpdate">
    </Image>
  </div>
</template>

<script>
import Image from "@/components/Image.vue";


export default {
  name: "ImageComparison",
  components: {
    Image
  },
  props: {
    images: {
      type: Array,
      default: () => []
    },
    scale: {
      type: Number,
      required: true
    },
    imageSize: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      offsetX: 0,
      showSlider: false // 控制slider过渡效果的显示
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
    moveHandler(e) {
      const parentWidth = this.$refs.slider.parentElement.offsetWidth;
      const newPosition = e.pageX - this.offsetX;

      // 检查移动的位置是否超出父元素的范围
      if (newPosition >= 0 && newPosition <= parentWidth) {
        this.$refs.slider.style.left = newPosition - 4 + "px";
        this.$refs.coverImage.style.width = newPosition + "px";
      }
    },
    onScaleUpdate(clampedScale) {
      this.$emit('update:scale', clampedScale);
    },
    onImageSizeUpdate(imageSize) {
      this.$emit('update:imageSize', imageSize);
    }
  }
};
</script>

<style scoped>
.image-comparison {
  width: 500px;
  height: 500px;
  /* overflow: hidden; */
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
  top: -15%;
  width: 6px;
  height: 130%;
  cursor: ew-resize;
  z-index: 20;
  background: rgba(255, 255, 255, 0.6);
}

.slider .before,
.after {
  width: 80px;
  height: 30px;
  line-height: 30px;
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  top: 12%;
  left: -90px;
  font-size: 20px;
  text-align: center;
  border-radius: 99px;
  cursor: default;
  color: #fff;
}

.after {
  left: 16px;
}

.image-comparison .slider .tag-icon {
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

.image-comparison .slider .tag-icon i {
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

