<script setup>
import { ref, watch } from "vue";

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue', 'focus']);

const inputValue = ref(props.modelValue);

const updateValue = () => {
  emit('update:modelValue', inputValue.value);
};

watch(() => props.modelValue, (newValue) => {
  inputValue.value = newValue;
});

</script>

<template>
  <input type="text" v-model="inputValue" placeholder="Введите текст..." class="input-field"
    @focus="emit('focus')" @input="updateValue">
</template>

<style scoped>
.input-field {
  margin-top: 10%;
  display: flex;
  justify-self: center;
  width: 50%;
  padding: 10px;
  border: 3px solid #313743;
  border-radius: 5px;
  transition: .5s ease;
}
</style>
