<script setup>
import { ref } from "vue";
import KeyItem from "./KeyItem.vue";
import KeyButtonLangs from "./KeyButtonLangs.vue";
import KeyButtonDelete from "./KeyButtonDelete.vue";

const emit = defineEmits(['keyPress', 'deleteAll']);
const props = defineProps(['inputValue']);

const capsLockEnabled = ref(false);
const shiftActive = ref(false);

// ФУНКЦИЯ ДЛЯ ОПРЕДЕЛЕНИЯ ОТОБРАЖАЕМОГО ЗНАЧЕНИЯ КЛАВИШИ
const displayedKeyValue = (key) => {
  // ОПРЕДЕЛЯЕТ, КАКОЕ ЗНАЧЕНИЕ ДОЛЖНО БЫТЬ ОТОБРАЖЕНО В ЗАВИСИМОСТИ ОТ СТАТУСА SHIFT И CAPS LOCK
  if (shiftActive.value && key.keyShift) {
    return key.keyShift;
  }
  if (capsLockEnabled.value && key.keyCaps) {
    return key.keyCaps;
  }
  return key.keyDisplay;
};

// ФУНКЦИЯ ДЛЯ ОБРАБОТКИ НАЖАТИЯ КЛАВИШИ
const handleKeyPress = (key) => {
  const keyValue = key.keyValue;
  let newValue = props.inputValue;

  switch (keyValue) {
    case "CapsLock":
      capsLockEnabled.value = !capsLockEnabled.value;
      break;
    case "Shift":
      shiftActive.value = !shiftActive.value;
      break;
    case "BackSpace":
      emit('deleteAll');
      newValue = newValue.slice(0, -1);
      break;
    case "Space":
      newValue += " ";
      break;
    default:
      if (keyValue !== "CapsLock" && keyValue !== "Shift") {
        newValue += displayedKeyValue(key);
      }
      break;
  }

  emit('keyPress', newValue);
};

const keyboardLayouts = ref({
  en: [
    [
      { keyValue: "`", keyDisplay: "`", keyShift: "~" },
      { keyValue: "1", keyDisplay: "1", keyShift: "!" },
      { keyValue: "2", keyDisplay: "2", keyShift: "@" },
      { keyValue: "3", keyDisplay: "3", keyShift: "#" },
      { keyValue: "4", keyDisplay: "4", keyShift: "$" },
      { keyValue: "5", keyDisplay: "5", keyShift: "%" },
      { keyValue: "6", keyDisplay: "6", keyShift: "^" },
      { keyValue: "7", keyDisplay: "7", keyShift: "&" },
      { keyValue: "8", keyDisplay: "8", keyShift: "*" },
      { keyValue: "9", keyDisplay: "9", keyShift: "(" },
      { keyValue: "0", keyDisplay: "0", keyShift: ")" },
      { keyValue: "-", keyDisplay: "-", keyShift: "_" },
      { keyValue: "=", keyDisplay: "=", keyShift: "+" },
      { keyValue: "BackSpace", keyDisplay: "BackSpace" },
    ],
    [
      { keyValue: "CapsLock", keyDisplay: "CapsLock" },
      { keyValue: "q", keyDisplay: "q", keyCaps: "Q" },
      { keyValue: "w", keyDisplay: "w", keyCaps: "W" },
      { keyValue: "e", keyDisplay: "e", keyCaps: "E" },
      { keyValue: "r", keyDisplay: "r", keyCaps: "R" },
      { keyValue: "t", keyDisplay: "t", keyCaps: "T" },
      { keyValue: "y", keyDisplay: "y", keyCaps: "Y" },
      { keyValue: "u", keyDisplay: "u", keyCaps: "U" },
      { keyValue: "i", keyDisplay: "i", keyCaps: "I" },
      { keyValue: "o", keyDisplay: "o", keyCaps: "O" },
      { keyValue: "p", keyDisplay: "p", keyCaps: "P" },
      { keyValue: "[", keyDisplay: "[", },
      { keyValue: "]", keyDisplay: "]", },
      { keyValue: "\\", keyDisplay: "\\", },
    ],
    [
      { keyValue: "Shift", keyDisplay: "Shift" },
      { keyValue: "a", keyDisplay: "a", keyCaps: "A" },
      { keyValue: "s", keyDisplay: "s", keyCaps: "S" },
      { keyValue: "d", keyDisplay: "d", keyCaps: "D" },
      { keyValue: "f", keyDisplay: "f", keyCaps: "F" },
      { keyValue: "g", keyDisplay: "g", keyCaps: "G" },
      { keyValue: "h", keyDisplay: "h", keyCaps: "H" },
      { keyValue: "j", keyDisplay: "j", keyCaps: "J" },
      { keyValue: "k", keyDisplay: "k", keyCaps: "K" },
      { keyValue: "l", keyDisplay: "l", keyCaps: "L" },
      { keyValue: ";", keyDisplay: ";", },
      { keyValue: "'", keyDisplay: "'", },
    ],
    [
      { keyValue: "z", keyDisplay: "z", keyCaps: "Z" },
      { keyValue: "x", keyDisplay: "x", keyCaps: "X" },
      { keyValue: "c", keyDisplay: "c", keyCaps: "C" },
      { keyValue: "v", keyDisplay: "v", keyCaps: "V" },
      { keyValue: "Space", keyDisplay: "Space" },
      { keyValue: "b", keyDisplay: "b", keyCaps: "B" },
      { keyValue: "n", keyDisplay: "n", keyCaps: "N" },
      { keyValue: "m", keyDisplay: "m", keyCaps: "M" },
      { keyValue: ",", keyDisplay: ",", },
      { keyValue: ".", keyDisplay: ".", },
      { keyValue: "/", keyDisplay: "/", },
    ],
  ],
  ru: [
    [
      { keyValue: "ё", keyDisplay: "ё", keyCaps: "Ё" },
      { keyValue: "1", keyDisplay: "1", keyShift: "~" },
      { keyValue: "2", keyDisplay: "2", keyShift: "!" },
      { keyValue: "3", keyDisplay: "3", keyShift: "@" },
      { keyValue: "4", keyDisplay: "4", keyShift: "#" },
      { keyValue: "5", keyDisplay: "5", keyShift: "$" },
      { keyValue: "6", keyDisplay: "6", keyShift: "^" },
      { keyValue: "7", keyDisplay: "7", keyShift: "&" },
      { keyValue: "8", keyDisplay: "8", keyShift: "*" },
      { keyValue: "9", keyDisplay: "9", keyShift: "(" },
      { keyValue: "0", keyDisplay: "0", keyShift: ")" },
      { keyValue: "-", keyDisplay: "-", keyShift: "_" },
      { keyValue: "=", keyDisplay: "=", keyShift: "+" },
      { keyValue: "BackSpace", keyDisplay: "BackSpace" },
    ],
    [
      { keyValue: "CapsLock", keyDisplay: "CapsLock" },
      { keyValue: "й", keyDisplay: "й", keyCaps: "Й" },
      { keyValue: "ц", keyDisplay: "ц", keyCaps: "Ц" },
      { keyValue: "у", keyDisplay: "у", keyCaps: "У" },
      { keyValue: "к", keyDisplay: "к", keyCaps: "К" },
      { keyValue: "е", keyDisplay: "е", keyCaps: "Е" },
      { keyValue: "н", keyDisplay: "н", keyCaps: "Н" },
      { keyValue: "г", keyDisplay: "г", keyCaps: "Г" },
      { keyValue: "ш", keyDisplay: "ш", keyCaps: "Ш" },
      { keyValue: "щ", keyDisplay: "щ", keyCaps: "Щ" },
      { keyValue: "з", keyDisplay: "з", keyCaps: "З" },
      { keyValue: "х", keyDisplay: "х", keyCaps: "Х" },
      { keyValue: "ъ", keyDisplay: "ъ", keyCaps: "Ъ" },
      { keyValue: "\\", keyDisplay: "\\" },
    ],
    [
      { keyValue: "Shift", keyDisplay: "Shift" },
      { keyValue: "ф", keyDisplay: "ф", keyCaps: "Ф" },
      { keyValue: "ы", keyDisplay: "ы", keyCaps: "Ы" },
      { keyValue: "в", keyDisplay: "в", keyCaps: "В" },
      { keyValue: "а", keyDisplay: "а", keyCaps: "А" },
      { keyValue: "п", keyDisplay: "п", keyCaps: "П" },
      { keyValue: "р", keyDisplay: "р", keyCaps: "Р" },
      { keyValue: "о", keyDisplay: "о", keyCaps: "О" },
      { keyValue: "л", keyDisplay: "л", keyCaps: "Л" },
      { keyValue: "д", keyDisplay: "д", keyCaps: "Д" },
      { keyValue: "ж", keyDisplay: "ж", keyCaps: "Ж" },
      { keyValue: "э", keyDisplay: "э", keyCaps: "Э" },
    ],
    [
      { keyValue: "я", keyDisplay: "я", keyCaps: "Я" },
      { keyValue: "ч", keyDisplay: "ч", keyCaps: "Ч" },
      { keyValue: "с", keyDisplay: "с", keyCaps: "С" },
      { keyValue: "м", keyDisplay: "м", keyCaps: "М" },
      { keyValue: "Space", keyDisplay: "Space" },
      { keyValue: "и", keyDisplay: "и", keyCaps: "И" },
      { keyValue: "т", keyDisplay: "т", keyCaps: "Т" },
      { keyValue: "ь", keyDisplay: "ь", keyCaps: "Ь" },
      { keyValue: "б", keyDisplay: "б", keyCaps: "Б" },
      { keyValue: "ю", keyDisplay: "ю", keyCaps: "Ю" },
      { keyValue: ".", keyDisplay: "." },
    ],
  ],
  de: [
    [
      { keyValue: "^", keyDisplay: "^", keyShift: "~" },
      { keyValue: "1", keyDisplay: "1", keyShift: "!" },
      { keyValue: "2", keyDisplay: "2", keyShift: "@" },
      { keyValue: "3", keyDisplay: "3", keyShift: "#" },
      { keyValue: "4", keyDisplay: "4", keyShift: "$" },
      { keyValue: "5", keyDisplay: "5", keyShift: "%" },
      { keyValue: "6", keyDisplay: "6", keyShift: "^" },
      { keyValue: "7", keyDisplay: "7", keyShift: "&" },
      { keyValue: "8", keyDisplay: "8", keyShift: "*" },
      { keyValue: "9", keyDisplay: "9", keyShift: "(" },
      { keyValue: "0", keyDisplay: "0", keyShift: ")" },
      { keyValue: "ß", keyDisplay: "ß", keyShift: "_" },
      { keyValue: "´", keyDisplay: "´", keyShift: "+" },
      { keyValue: "BackSpace", keyDisplay: "BackSpace" },
    ],
    [
      { keyValue: "CapsLock", keyDisplay: "CapsLock" },
      { keyValue: "q", keyDisplay: "q", keyCaps: "Q" },
      { keyValue: "w", keyDisplay: "w", keyCaps: "W" },
      { keyValue: "e", keyDisplay: "e", keyCaps: "E" },
      { keyValue: "r", keyDisplay: "r", keyCaps: "R" },
      { keyValue: "t", keyDisplay: "t", keyCaps: "T" },
      { keyValue: "z", keyDisplay: "z", keyCaps: "Z" },
      { keyValue: "u", keyDisplay: "u", keyCaps: "U" },
      { keyValue: "i", keyDisplay: "i", keyCaps: "I" },
      { keyValue: "o", keyDisplay: "o", keyCaps: "O" },
      { keyValue: "p", keyDisplay: "p", keyCaps: "P" },
      { keyValue: "ü", keyDisplay: "ü", keyCaps: "Ü" },
      { keyValue: "+", keyDisplay: "+" },
      { keyValue: "<", keyDisplay: "<" },
    ],
    [
      { keyValue: "Shift", keyDisplay: "Shift" },
      { keyValue: "a", keyDisplay: "a", keyCaps: "A" },
      { keyValue: "s", keyDisplay: "s", keyCaps: "S" },
      { keyValue: "d", keyDisplay: "d", keyCaps: "D" },
      { keyValue: "f", keyDisplay: "f", keyCaps: "F" },
      { keyValue: "g", keyDisplay: "g", keyCaps: "G" },
      { keyValue: "h", keyDisplay: "h", keyCaps: "H" },
      { keyValue: "j", keyDisplay: "j", keyCaps: "J" },
      { keyValue: "k", keyDisplay: "k", keyCaps: "K" },
      { keyValue: "l", keyDisplay: "l", keyCaps: "L" },
      { keyValue: "ö", keyDisplay: "ö", keyCaps: "Ö" },
      { keyValue: "ä", keyDisplay: "ä", keyCaps: "Ä" },
      { keyValue: "#", keyDisplay: "#", },
    ],
    [
      { keyValue: "y", keyDisplay: "y", keyCaps: "Y" },
      { keyValue: "x", keyDisplay: "x", keyCaps: "X" },
      { keyValue: "c", keyDisplay: "c", keyCaps: "C" },
      { keyValue: "v", keyDisplay: "v", keyCaps: "V" },
      { keyValue: "Space", keyDisplay: "Space" },
      { keyValue: "b", keyDisplay: "b", keyCaps: "B" },
      { keyValue: "n", keyDisplay: "n", keyCaps: "N" },
      { keyValue: "m", keyDisplay: "m", keyCaps: "M" },
      { keyValue: ",", keyDisplay: "," },
      { keyValue: ".", keyDisplay: "." },
      { keyValue: "-", keyDisplay: "-" },
    ],
  ],
}
)

// УСТАНАВЛИВАЕТ АНГЛИЙСКУЮ РАСКЛАДКУ ПО УМОЛЧАНИЮ
const currentLayout = ref('en');

// ФУНКЦИЯ ДЛЯ СМЕНЫ РАСКЛАДКИ КЛАВИАТУРЫ
const changeLayout = (layout) => {
  currentLayout.value = layout;
};

// ОПРЕДЕЛЕНИЕ СПЕЦИАЛЬНЫХ КЛАВИШ С ШИРИНАМИ
const specialKeys = {
  BackSpace: "key-wide",
  CapsLock: "key-wide",
  Shift: "key-wide",
  Space: "key-space",
};

// ФУНКЦИЯ ДЛЯ ПРОВЕРКИ, АКТИВНА ЛИ КЛАВИША
const isKeyActive = (keyValue) => {
  return (keyValue === 'CapsLock' && capsLockEnabled.value) ||
    (keyValue === 'Shift' && shiftActive.value);
};
</script>

<template>
  <div class="keyboard">
    <div v-for="row in keyboardLayouts[currentLayout]" :key="row" class="keyboard-row">
      <KeyItem v-for="item in row" :key="item" :displayedKeyValue="displayedKeyValue(item)"
        :isActive="isKeyActive(item.keyValue)" :specialClass="specialKeys[item.keyValue]"
        @keyPress="handleKeyPress(item)" />
    </div>
    <KeyButtonLangs @changeLayout="changeLayout" />
    <KeyButtonDelete @deleteAll="emit('deleteAll')" />
  </div>
</template>

<style scoped>
.keyboard {
  position: fixed;
  bottom: 0;
  width: 100%;
  padding: 2% 2% 3% 2%;
  background: #3137438e;
  animation-name: keyboardUp;
  animation-duration: 1s
}

@keyframes keyboardUp {
  0% {
    opacity: 0;
    transform: translateY(300px);
  }

  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.keyboard-row {
  display: flex;
}
</style>
