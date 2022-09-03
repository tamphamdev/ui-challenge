<script setup>
import { ref } from "vue";
import Detail from "./components/Detail.vue";
import Header from "./components/Header.vue";
import SideBarVue from "./components/SideBar.vue";
const currentEmployee = ref({});
const handleSetCurrentEmployee = (employee) => {
  currentEmployee.value = employee;
};
</script>

<template>
  <Header />
  <Suspense>
    <SideBarVue
      @handleSetCurrentEmployee="handleSetCurrentEmployee"
      :currentEmployee="currentEmployee"
    />
  </Suspense>
  <div class="main">
    <Detail
      :currentEmployee="currentEmployee"
      @handleSetCurrentEmployee="handleSetCurrentEmployee"
    />
  </div>
</template>

<style lang="scss" scoped>
#app {
  height: 100vh;
  padding: 0;
}
* {
  margin: 0;
  padding: 0;
}
html,
body {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  font-size: 62.5%; //10px per rem
}
.main {
  margin-left: 30%;
  height: 100%;
  background-color: #2e2e36;
}
</style>
