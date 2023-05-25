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
    <div class="option-bar">
      <button
        v-for="(option, index) in options"
        :key="index"
        :class="{ chosen: index === selectedOption }"
        @click="selectOption(index)"
      >
        {{ option }}
      </button>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const props = defineProps({
    title: {
      type: String,
      required: true
    },
    description: {
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
    }
  });
  
  const selectedOption = ref(0);
  
  function selectOption(index) {
    selectedOption.value = index;
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
  </style>
  