<script setup>
const emit = defineEmits(['deleteAll']);

// ФУНКЦИЯ ДЛЯ УДАЛЕНИЯ ВСЕГО
const deleteAll = () => {
  emit('deleteAll');
};
</script>

<template>
  <button
    @click="deleteAll"
    class="key delete-btn"
    aria-label="Удалить все">
    &#128465; Delete all
  </button>
</template>

<style scoped>

</style>
