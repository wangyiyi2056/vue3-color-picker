<template>
  <div class="ck-cp-local-color-conatiner intrinsic">
    <div class="ck-cp-color-list">
      <div
        class="ck-cp-color-bg"
        v-for="item in intrinsicColorList"
        :key="`color-${item.color}`"
      >
        <div
          class="ck-cp-color-item"
          :class="item.selected ? 'ck-select' : ''"
          :style="{ background: item.color }"
          @click="setSelectColor(item.color)"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { ref, onBeforeMount } from "vue";
  const props = defineProps({
    intrinsicColorList: { default: "", type: Array as () => string[] },
  });

  const emits = defineEmits<{
    (e: "color-item-click", color: string): void;
  }>();

  interface ListItem {
    color: string;
    selected: boolean;
  }
  const intrinsicColorList = ref<ListItem[]>([]);

  const setSelectColor = (color: string) => {
    intrinsicColorList.value.forEach((item) => {
      if (item.color === color) {
        item.selected = !item.selected;
      } else {
        item.selected = false;
      }
    });
    emits("color-item-click", color);
  };

  onBeforeMount(() => {
    let list: string[] = props.intrinsicColorList;
    intrinsicColorList.value = list!.map((item) => {
      return {
        color: item,
        selected: false,
      };
    });
  });
</script>

<style></style>
