<template>
  <div
    v-bind="$attrs"
    class="menu-item"
    :style="{fontSize: style}"
    @click.stop="onSelectEmployee"
  >
    <a
      href="#"
      style="color: inherit"
    > {{menuItem}} </a>
  </div>
</template>

<script setup>
import { computed } from "@vue/runtime-core";
const BASE_ON_POPULARITY = 5;
const props = defineProps({
  item: Object,
});

const menuItem = computed(() => props?.item?.name);
const style = computed(
  () => props?.item?.popularity * BASE_ON_POPULARITY + "px"
);
</script>

<style lang="scss" scoped>
.menu-item {
  cursor: pointer;
  margin: 1rem 0;
  color: #fff;
}
</style>