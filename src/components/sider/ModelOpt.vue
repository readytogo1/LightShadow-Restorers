<template>
    <div class="title-bar">
      <div class="logo" :style="{ backgroundColor: logoColor }">
        <i :class="logoIcon"></i>
      </div>
      <div class="title-wrapper">
        <h2 class="title">{{ title }}</h2>
        <span class="desc">{{ description }}</span>
      </div>
    </div>
    <div class="option-bar" v-if="typeOpt === 0">
      <button
        v-for="(option, index) in options"
        :key="index"
        :class="{ chosen: index === selectedOption }"
        @click="selectOption(index)"
      >
        {{ option }}
      </button>
    </div>
    <div class="combo-wrapper" v-else>
      <div class="combo" @click="toggleRotation">
        <div class="brush-wrapper">
          <i class="ri-brush-line"></i>
        </div>
        <span>{{desc}}</span>
        <button class="rotate-btn" :class="rotationClass" >
          <i class="ri-arrow-right-s-line"></i>
        </button>
      </div>

      <div class="list-wrapper" v-if="isRotating">
        <button
          v-for="(option, index) in options"
          :key="index"
          :class="{ chosen: index === selectedOption }"
          @click="selectOption(index)"
        >
          <img :src="optionsImg[index]" alt="">
          <p>{{ option }}</p>
        </button>
      </div>  
    </div>
    
  </template>
  
  <script setup>
  import { ref,computed } from 'vue';
  const emits = defineEmits(['selected']);
  const props = defineProps({
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    desc: {
      type: String,
      required: true
    },
    logoIcon: {
      type: String,
      required: true
    },
    logoColor: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      required: true
    },
    optionsImg: {
      type: Array
    },
    typeOpt: {
      type: Number,
      default:0
    }
  });
  
  const selectedOption = ref(0);
  
  const isRotating = ref(false);

  const rotationClass = computed(() => {
    return isRotating.value ? 'rotate' : '';
  });
  function toggleRotation() {
    isRotating.value = !isRotating.value;
  }
  function selectOption(index) {
    selectedOption.value = index;
    // 触发自定义事件，并将选中的索引作为参数传递给父组件
    emits('selected', index);
  }
  </script>
  
  <style scoped>
  .title-bar {
    display: flex;
    align-items: center;
    margin-top: 10px;
  }
  
  .logo {
    width: 40px;
    height: 40px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-right: 20px;
  }
  
  i {
    color: #fff;
    font-size: 32px;
  }
  
  .title-wrapper h2 {
    color: #dcdcdc;
    font-size: 16px;
    margin-bottom: 2px;
  }
  
  .title-wrapper .desc {
    color: #b1b1b8;
    font-size: 15px;
  }
  
  .option-bar button {
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
  
  .option-bar .chosen {
    background-color: #353539;
    transition: 0.3s;
  }
  
  .option-bar {
    border-bottom: 1px solid #2a2a2e;
    padding-bottom: 20px;
  }
  .combo-wrapper{
    margin-bottom: 50px;
  }
  .combo{
    margin: 20px 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 40px;
  }
  .combo:hover{
    background-color: rgba(255, 255, 255, .1);
    border-radius: 10px;
    cursor: pointer;
  }
  .combo i{
    color: #d7d8e2;
    font-size: 20px;
  }
  .combo span{
    color: #d7d8e2;
    margin-left: -60px;
  }
  .combo .brush-wrapper{
    background-color: #353539;
    border-radius: 5px;
    width: 32px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .rotate-btn {
  background-color: transparent;
  border: none;
  outline: none;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.rotate-btn.rotate {
  transform: rotate(90deg);
}
.list-wrapper{
  display: flex;
  text-align: center;
  justify-content: space-between;
}
.list-wrapper button{
  background-color: #222226;
  border: none;
}
.list-wrapper button.chosen img{
  border: 2px solid white;
}
.list-wrapper img{
  border-radius: 10px;
  background-color: #2b2b2f;
  width: 60px;
  height: 60px;
  border: 2px solid #222226;
}
.list-wrapper p{
  color: #b1b1b8;
  font-size: 10px;
  font-weight: bold;
}
  </style>
  