<template>
  <div class="detail">
    <div
      class="detail__container"
      v-if="char"
    >
      <div class="detail__left">
        <div class="character__thumb">
          <img
            class="character__thumb__img"
            :src="`/assets/images/${char.image}`"
            alt="thumb"
          >
        </div>
      </div>
      <div class="detail__right">
        <h1 class="character__name">{{char.name}}</h1>
        <div class="character__popularity">
          <label for="popularity">Popularity</label>
          <input
            type="range"
            min="1"
            max="10"
            class="slider"
            v-model="char.popularity"
            id="popularity"
            @change="handleChangeFontSize"
          >
        </div>
        <div class="character__bio">
          <h3>Biography</h3>
          <p class="character__bio--content">{{char.biography}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";
const props = defineProps({
  currentEmployee: Object,
});
const emit = defineEmits(["handleSetCurrentEmployee"]);

const handleChangeFontSize = () => {
  const payload = { ...char.value, popularity: char.value.popularity };
  emit("handleSetCurrentEmployee", payload);
};
const char = computed(() => {
  return props.currentEmployee;
});
</script>

<style lang="scss" scoped>
.detail {
  color: #fff;
  max-width: 80%;
  width: 100%;
  margin: auto;
  &__container {
    display: flex;
  }
  &__left {
    width: 30%;
    margin-top: -3rem;
    margin-right: 1.5rem;
  }
  &__right {
    margin-top: -3rem;
    margin-left: 1.5rem;
    text-align: left;
  }
}
.character {
  &__thumb {
    width: 150px;
    height: 150px;
    border: 1px solid #fff;
    border-radius: 4px;
    filter: drop-shadow(10px 10px 10px rgb(0 0 0));
    &__img {
      width: 100%;
    }
  }

  &__name {
    margin: 0;
  }

  &__popularity {
    margin-top: 3rem;
    display: flex;
    align-items: center;
    label {
      margin-right: 2rem;
    }
  }

  &__bio {
    margin-top: 2rem;
    background: #1a1d24;
    padding: 1rem;
    border-radius: 4px;
    h3 {
      margin-top: 0;
    }
  }
}

.slider {
  -webkit-appearance: none; /* Override default CSS styles */
  appearance: none;
  width: 100%;
  height: 5px;
  background: #000;
  outline: none;
  transition: opacity 0.2s;
  border-radius: 4px;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  border-radius: 50%;
  width: 1.5rem;
  height: 1.5rem;
  background: #fff;
  box-shadow: -2px 5px 5px #000;
  cursor: pointer;
}
</style>