<script setup>
import { ref, onBeforeMount, onBeforeUnmount } from "vue";
import InputField from "./components/InputField.vue";
import KeyboardContainer from "./components/KeyboardContainer.vue";

const inputValues = ref({
  input1: '',
  input2: '',
  input3: ''
});

const isKeyboardVisible = ref(false);
const activeInputId = ref(null);

const onInputFocus = (id) => {
  activeInputId.value = id;
  isKeyboardVisible.value = true; // ПОКАЗЫВАЕТ КЛАВИАТУРУ ПРИ ФОКУСЕ
};

const onDocumentClick = (e) => {
  // ПРОВЕРЯЕТ КЛИК ПО КЛАВИАТУРЕ, ПОЛЕ ВВОДА, КНОПКЕ
  if (e.target.closest('.keyboard') || e.target.closest('.input-field') || e.target.closest('.btn-layout')) {
    return;
  }
  isKeyboardVisible.value = false;
};

// РЕГИСТРАЦИЯ ОБРАБОТЧИКА СОБЫТИЙ ПРИ МОНТАЖЕ КОМПОНЕНТА
onBeforeMount(() => {
  document.addEventListener('click', onDocumentClick);
});

// УДАЛЕНИЕ ОБРАБОТЧИКА СОБЫТИЙ ПРИ УДАЛЕНИИ КОМПОНЕНТА
onBeforeUnmount(() => {
  document.removeEventListener('click', onDocumentClick);
});

const updateInputValue = (id, value) => {
  inputValues.value[id] = value;
};
</script>

<template>
  <div>
    <InputField v-model="inputValues['input1']" @focus="() => onInputFocus('input1')" />
    <InputField v-model="inputValues['input2']" @focus="() => onInputFocus('input2')" />
    <InputField v-model="inputValues['input3']" @focus="() => onInputFocus('input3')" />
    <Transition name="keyboard">
      <KeyboardContainer
        v-if="isKeyboardVisible"
        :inputValue="inputValues[activeInputId]"
        @deleteAll="updateInputValue(activeInputId, '')"
        @keyPress="(value) => updateInputValue(activeInputId, value)"
      />
    </Transition>
  </div>
</template>

<style scoped>

@keyframes keyboardDown {
  0% {
    opacity: 1;
    transform: translateY(0);
  }

  100% {
    opacity: 0;
    transform: translateY(300px);
  }
}

.keyboard-enter-active,
.keyboard-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.keyboard-enter,
.keyboard-leave-to {
  opacity: 0;
  transform: translateY(300px);
}

.btn-showed {
  border-radius: 20px;
  padding: 15px;
  background: #313743;
  margin-top: 30px;
  font-size: 15px;
  text-transform: uppercase;
  display: flex;
  justify-self: center;
  font-weight: 500;
  color: white;
  transition: padding .5s ease, font-weight .5s ease;
}

.btn-showed:hover {
  padding: 17px;
  font-weight: 700;
}
</style>
