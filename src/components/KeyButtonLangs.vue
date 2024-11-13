<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue';

const emit = defineEmits(['changeLayout']);

// ДОСТУПНЫЕ РАСКЛАДКИ
const layouts = ['en', 'ru', 'de'];
// УСТАНАВЛИВАЕТ АНГЛИЙСКУЮ РАСКЛАДКУ ПО УМОЛЧАНИЮ
const currentLayout = ref(layouts[0]);
// ИНИЦИАЛИЗАЦИЯ СТАТУСА ВИДИМОСТИ МЕНЮ
const isMenuVisible = ref(false);

// ФУНКЦИЯ ДЛЯ ПЕРЕКЛЮЧЕНИЯ ВИДИМОСТИ МЕНЮ
const toggleMenu = () => {
  isMenuVisible.value = !isMenuVisible.value;
};

// ФУНКЦИЯ ДЛЯ ВЫБОРА РАСКЛАДКИ
const selectLayout = (layout) => {
  currentLayout.value = layout;
  emit('changeLayout', layout);
  isMenuVisible.value = false;
};

const currentLayoutLabel = computed(() => currentLayout.value.toUpperCase());

// ФУНКЦИЯ ДЛЯ ОБРАБОТКИ КЛИКОВ ЗА ПРЕДЕЛАМИ МЕНЮ
const handleClickOutside = (event) => {
  const menu = document.querySelector('.layout-menu');
  const button = document.querySelector('.key-langs');
  if (isMenuVisible.value && menu && !menu.contains(event.target) && !button.contains(event.target)) {
    isMenuVisible.value = false;
  }
};


onMounted(() => {
  document.addEventListener('click', handleClickOutside);
});

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside);
});
</script>

<template>
  <button @click="toggleMenu" class="key key-langs">
    <img src="../img/lang-icon.png" class="lang-icon">
    {{ currentLayoutLabel }}
  </button>
  <div v-if="isMenuVisible" class="menu-layout" role="menu">
    <button v-for="layout in layouts" :key="layout" @click="selectLayout(layout)" class="btn-layout">
      {{ layout }}
    </button>
  </div>
</template>

<style scoped>
.menu-layout{
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
