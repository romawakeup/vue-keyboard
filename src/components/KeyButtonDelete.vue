<script setup>
const emit = defineEmits(['deleteAll']);

// ФУНКЦИЯ ДЛЯ УДАЛЕНИЯ
const deleteAll = () => {
  emit('deleteAll');
};
</script>

<template>
  <button @click="deleteAll" class="key delete-btn">
    &#128465; Delete all
  </button>
</template>

<style scoped></style>
