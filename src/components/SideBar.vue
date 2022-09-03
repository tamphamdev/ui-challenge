<template>
  <div class="sidebar">
    <div class="sidebar__logo">
      <img
        :src="Logo"
        alt=""
      >
    </div>
    <div
      class="sidebar__menu"
      v-for="(menu,index) in  menuItems.employees"
      :key="index"
      :class="{active : currentEmployee.name === menu.name, sameColleagues: hasSameColleagues}"
    >
      <MenuItem
        :item="menu"
        :class="{'text-active': currentEmployee.name === menu.name, 'same-colleagues' : hasSameColleagues(menu)}"
        @click.stop="onSelectEmployee(menu)"
      />
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import MenuItem from "./MenuItem.vue";
import Logo from "/assets/logo/the-godfather.svg";

const emit = defineEmits(["handleSetCurrentEmployee"]);
const props = defineProps({
  currentEmployee: Object,
});

let menuItems = ref([]);

const res = await fetch("/data/EmployeeData.json");
menuItems = await res.json();
// NOTE: The json file only have 4 employees => not match with the design.

const currentEmployee = computed(() => {
  const index = menuItems.employees.findIndex(
    (e) => e.name === props?.currentEmployee.name
  );
  if (index !== -1) {
    menuItems.employees.splice(index, 1, props?.currentEmployee);
    onSelectEmployee(props?.currentEmployee);
  }
  return props?.currentEmployee;
});

const onSelectEmployee = (employee) => {
  emit("handleSetCurrentEmployee", employee);
};

const hasSameColleagues = (employee) => {
  if (!currentEmployee.value) return;

  return currentEmployee.value?.colleagues?.includes(employee.name);
};

onMounted(() => {
  if (menuItems?.employees?.length) {
    onSelectEmployee(menuItems.employees[0]);
  }
});
</script>

<style lang="scss" scoped>
.sidebar {
  position: absolute;
  top: 0;
  left: 0;
  width: 30%;
  height: 100%;
  z-index: 1;
  &:before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0.1;
    background: #000;
    z-index: -1;
  }
  &__logo {
    max-height: 30vh;
    height: 320px;
    width: 100%;
    position: relative;
    z-index: 1;
    img {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }
  }
}
.active {
  background: #404146;
  padding: 0.5rem;
}
.text-active,
.same-colleagues {
  color: #3eabcb !important;
}
</style>