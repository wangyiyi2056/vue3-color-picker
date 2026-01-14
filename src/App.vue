<script setup lang="ts">
  import { ref } from "vue";
  import Vue3ColorPicker from "./components/Vue3ColorPicker.vue";

  const iscolor1 = ref(false);
  const color1 = ref("");
  const inputColor = ref("");

  const handleModel = (e: string) => {
    document.body.style.background = e;
    inputColor.value = e; // 同步到输入框
  };

  const applyInputColor = () => {
    color1.value = inputColor.value; // 回车或失焦时应用颜色
  };
</script>

<template>
  <input
    v-model="inputColor"
    @focus="iscolor1 = true"
    @blur="applyInputColor"
    @keyup.enter="applyInputColor"
  />

  <p
    style="color: #ccc; width: 100px; height: 100px"
    :style="{ background: color1 }"
  >
    {{ color1 }}
  </p>
  <Vue3ColorPicker
    style="position: absolute; top: 0; right: 0; left: auto"
    v-if="iscolor1"
    v-model="color1"
    theme="light"
    mode="solid"
    @update:model-value="handleModel"
    :show-picker-mode="true"
    :show-input-menu="true"
    :show-color-list="true"
    :show-eye-drop="true"
    input-type="RGB"
    type="HEX8"
    :disabled="false"
    :local="{
      angle: '角度',
      positionX: '位置X',
      positionY: '位置Y',
      solid: '实体',
      gradient: '渐变',
      linear: '线性',
      radial: '径向',
      colorPalette: '调色板',
    }"
  />
</template>

<style>
  body {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>
