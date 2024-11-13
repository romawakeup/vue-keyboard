<script setup>

const emit = defineEmits(['keyPress']);

const props = defineProps({
  keyData: Object,
  displayedKeyValue: String,
  isActive: Boolean,
  specialClass: String,
});

const handleKeyPress = () => {
  emit('keyPress', props.keyData);
};
</script>

<template>
  <div @click="handleKeyPress" class="key" :class="[specialClass, { 'key-active': isActive }]">
    {{ displayedKeyValue }}
  </div>
</template>

<style>
.key {
  border-radius: 5px;
  padding: 10px;
  margin: 5px;
  cursor: pointer;
  flex: 1;
  background: white;
  text-align: center;
}

.key:hover {
  background: #CCEA58;
  color: white;
  font-weight: 700;
  animation: keyPress .3s ease;
}

@keyframes keyPress {
  0% {
    transform: scale(1);
  }

  25% {
    transform: scale(0.925);
  }

  50% {
    transform: scale(0.95);
  }

  75% {
    transform: scale(0.975);
  }

  100% {
    transform: scale(1);
  }
}

.key-wide {
  flex: 2;
}

.key-space {
  flex: 5;
}

.key-active {
  background-color: #C68DFE;
  color: white;
}
</style>
