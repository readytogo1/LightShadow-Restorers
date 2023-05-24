<!-- <template>
    <div>
      <div class="image-container" ref="container" @wheel="handleWheel">
        <img :src="imageUrl" :style="{ transform: `scale(${scale})` }" @mousedown="handleMouseDown" @mousemove="handleMouseMove" @mouseup="handleMouseUp" @mouseleave="handleMouseLeave" @load="updateImageSize">
      </div>
      <div class="slider-container">
        <input type="range" min="0.1" max="2.5" step="0.1" v-model="scale" class="slider" @input="handleScaleInput">
        <span>当前尺寸：{{ imageSize.width }}px × {{ imageSize.height }}px，缩放比例：{{ (scale * 100).toFixed(0) }}%</span>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, reactive, onMounted, onUnmounted, computed } from 'vue';
  
  export default {
    setup() {
      const imageUrl = '/img/1.jpg';
      const scale = ref(1);
      const isDragging = ref(false);
      const startMouseX = ref(0);
      const startScale = ref(0);
  
      const imageSize = reactive({
        width: 0,
        height: 0,
      });
  
      /* const handleWheel = (event) => {
        event.preventDefault();
        const delta = Math.sign(event.deltaY);
        updateScale(delta);
      }; */
  
      const handleMouseDown = (event) => {
        isDragging.value = true;
        startMouseX.value = event.clientX;
        startScale.value = scale.value;
      };
  
      const handleMouseMove = (event) => {
        if (isDragging.value) {
          const diffX = event.clientX - startMouseX.value;
          const scaleDelta = diffX * 0.01;
          updateScale(scaleDelta + startScale.value);
        }
      };
  
      const handleMouseUp = () => {
        isDragging.value = false;
      };
  
      const handleMouseLeave = () => {
        isDragging.value = false;
      };
  
      /* const updateScale = (newScale) => {
        scale.value = Math.min(Math.max(newScale, 0.1), 2.5) ;
      }; */
  
      const handleScaleInput = () => {
        scale.value = Math.min(Math.max(scale.value, 0.1), 2.5);
      };

  
      const refContainer = ref(null);
  
      const updateImageSize = () => {
        const container = refContainer.value;
        const image = new Image();
        image.src = imageUrl;
        image.onload = () => {
          imageSize.width = image.width;
          imageSize.height = image.height;
        };
      };
  
      onMounted(() => {
        const container = refContainer.value;
        if (container) {
            container.addEventListener('wheel', handleWheel);
        }
        updateImageSize();
        addWheelListener();
      });

      onUnmounted(() => {
        const container = refContainer.value;
        if (container) {
            container.removeEventListener('wheel', handleWheel);
        }
        removeWheelListener();
      });
      const addWheelListener = () => {
      document.addEventListener('wheel', handleWheel, { passive: false });
    };

    const removeWheelListener = () => {
      document.removeEventListener('wheel', handleWheel);
    };

    const handleWheel = (event) => {
      if (event.ctrlKey) {
        event.preventDefault();

        const delta = getWheelDelta(event);
        updateScale(delta);
      }
    };

    const getWheelDelta = (event) => {
      let delta = 0;

      if (event.deltaMode === 0) {
        // DOM_DELTA_PIXEL
        delta = event.deltaY;
      } else if (event.deltaMode === 1) {
        // DOM_DELTA_LINE
        delta = event.deltaY * 40;
      } else if (event.deltaMode === 2) {
        // DOM_DELTA_PAGE
        delta = event.deltaY * window.innerHeight;
      }

      return -Math.sign(delta);
    };

    const updateScale = (delta) => {
      const newScale = scale.value + delta * 0.1;

      // 控制缩放比例在 10% 到 250% 之间
      scale.value = Math.max(Math.min(newScale, 2.5), 0.1);
    };
  
      return {
        imageUrl,
        scale,
        imageSize,
        handleMouseDown,
        handleMouseMove,
        handleMouseUp,
        handleMouseLeave,
        refContainer,
        updateImageSize,
        handleScaleInput,
      };
    },
  };
  </script>
  
  <style>
  .image-container {
    width: 100%;
    height: 500px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .image-container img {
    user-select: none;
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
    <div>
      <Image :imageUrl="imageUrl" :scale="scale" @update:imageSize="imageSize = $event" @update:scale="scale = $event"></Image>
      <ZoomControls :scale="scale" :imageSize="imageSize" @update:scale="scale = $event"></ZoomControls>
    </div>
  </template>
  
  <script>
  import Image from './Image.vue';
  import ZoomControls from './ZoomControls.vue';
  
  export default {
    components: {
      Image,
      ZoomControls,
    },
    data() {
      return {
        imageUrl: '/img/3.jpg',
        scale: 1,
        imageSize: {
          width: 0,
          height: 0,
        },
      };
    },
  };
  </script>
  
  