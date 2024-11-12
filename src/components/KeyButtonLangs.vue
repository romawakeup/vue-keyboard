<script setup>
import { ref, computed } from 'vue';

const emit = defineEmits(['changeLayout']); // ЭМИТАЦИЯ СОБЫТИЙ

const layouts = ['en', 'ru', 'de']; // ДОСТУПНЫЕ РАСКЛАДКИ
const currentLayout = ref(layouts[0]);
const isMenuVisible = ref(false); // ДЛЯ ВИДИМОСТИ РАСКЛАДКИ

// ФУНКЦИЯ ДЛЯ ПЕРЕКЛЮЧЕНИЯ ВИДИМОСТИ МЕНЮ ЯЗЫКОВ
const toggleMenu = () => {
  isMenuVisible.value = !isMenuVisible.value;
};

// ФУНКЦИЯ ДЛЯ ВЫБОРА ЯЗЫКОВ
const selectLayout = (layout) => {
  currentLayout.value = layout;
  emit('changeLayout', layout);
  isMenuVisible.value = false;
};


const currentLayoutLabel = computed(() => {
  return currentLayout.value.toUpperCase();
});
</script>

<template>
  <button @click="toggleMenu" class="key key-langs" :aria-expanded="isMenuVisible.toString()"
    aria-label="Переключить языковое меню">
    <img src="../img/lang-icon.png" class="lang-icon">
    {{ currentLayoutLabel }}
  </button>
  <div v-if="isMenuVisible" class="layout-menu">
    <button v-for="layout in layouts" :key="layout" @click="selectLayout(layout)" class="btn-layout">
      {{ layout }}
    </button>
  </div>

</template>

<style scoped>
.layout-menu {
  position: absolute;
  left: 2.3%;
  border-radius: 5px;
  background: white;

}

.btn-layout {
  border-radius: 5px;
  padding: 5px;
  margin: 5px;
  cursor: pointer;
  background: white;
  text-transform: uppercase;
  font-size: 20px;
}

.key-langs {
  flex: 1;
}

.btn-layout:hover {
  background: #CCEA58;
  color: white;
  animation: keyPress .3s ease;
  font-weight: 500;
}
</style>
