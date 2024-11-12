<script setup>
import { ref, computed } from "vue";
import InputField from "./components/InputField.vue";
import KeyboardContainer from "./components/KeyboardContainer.vue";

const inputValue = ref("");
const capsLockEnabled = ref(false);
const isShowed = ref(false);
const shiftActive = ref(false);



// ФУНКЦИЯ ДЛЯ ПЕРЕКЛЮЧЕНИЯ ВИДИМОСТИ КЛАВИАТУРЫ
const toggleKeyboard = () => {
  isShowed.value = !isShowed.value;
};

// ФУНКЦИЯ ДЛЯ ОТОБРАЖЕНИЯ ЗНАЧЕНИЯ ВВОДА
const displayValue = computed(() => {
  return inputValue.value;
});
const clearInput = () => {
  inputValue.value = "";
}

// ФУНКЦИЯ ДЛЯ ОТОБРАЖЕНИЯ ЗНАЧЕНИЙ КЛАВИШ
const displayedKeyValue = (key) => {
  if (shiftActive.value && key.keyShift) {
    return key.keyShift;
  }

  if (capsLockEnabled.value && key.keyCaps) {
    return key.keyCaps;
  }

  return key.keyDisplay;
};

// ФУНКЦИЯ ДЛЯ ОБРАБОТКИ СПЕЦИАЛЬНЫХ КЛАВИШ
const handleKeyPress = (key) => {
  const keyValue = key.keyValue; // Используем keyValue вместо displayedKeyValue
  switch (keyValue) {
    case "CapsLock":
      capsLockEnabled.value = !capsLockEnabled.value; // ПЕРЕКЛЮЧАЕМ КАПС ЛОК
      break;
    case "Shift":
      shiftActive.value = !shiftActive.value; // ВКЛЮЧАЕМ ВЫКЛЮЧАЕМ ШИФТ
      break;
    case "BackSpace":
      inputValue.value = inputValue.value.slice(0, -1); // УДАЛЯЕМ ПОСЛЕДНИЙ СИМВОЛ
      break;
    case "Space":
      inputValue.value += " "; // ДОБАВЛЯЕТ ПРОБЕЛ
      break;
    default:
      if (keyValue !== "CapsLock" && keyValue !== "Shift") {
        inputValue.value += displayedKeyValue(key);
      }
      break;
  }
};
</script>

<template>
  <div>
    <InputField v-model="displayValue" />
    <button @click="toggleKeyboard" class="btn-showed">Открыть/закрыть клавиатуру</button>
    <transition name="keyboard">
      <KeyboardContainer v-if="isShowed" @keyPress="handleKeyPress" @deleteAll="clearInput" :capsLockEnabled="capsLockEnabled"
        :shiftActive="shiftActive" :displayedKeyValue="displayedKeyValue"  />
    </transition>
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
