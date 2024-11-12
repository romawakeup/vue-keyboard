<script setup>
import { ref } from "vue";
import KeyButtonLangs from "./KeyButtonLangs.vue";
import KeyButtonDelete from "./KeyButtonDelete.vue"


const emit = defineEmits(['keyPress']);
const props = defineProps(['capsLockEnabled', 'shiftActive', 'displayedKeyValue']);



// РАССКЛАДКИ ЯЗЫКОВ ДЛЯ КЛАВИАТУРЫ
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

// ПЕРВОНАЧАЛЬНАЯ РАССКЛАДКА КЛАВЫ ПРИ ОТКРЫТИИ
const currentLayout = ref('en');

// ФУНКЦИЯ ДЛЯ СМЕНЫ РАСКЛАДКИ КЛАВЫ
const changeLayout = (layout) => {
  currentLayout.value = layout;
};

// ФУНКЦИЯ ДЛЯ ОБРАБОТКИ НАЖАТИЙ КЛАВИШ
const handleKeyPress = (key) => {
  emit('keyPress', key); // ЭМИТИРИУЕМ ОБЪЕКТ КЛАВИШИ
};

const hadleDeleteAll = () => {
  emit('deleteAll'); // ЭМИТИРИУЕМ ОБЪЕКТ КЛАВИШИ
};


// СПЕЦАИЛЬНЫЕ КЛАВИШИ
const specialKeys = {
  BackSpace: "key-wide",
  CapsLock: "key-wide",
  Shift: "key-wide",
  Space: "key-space",
};

</script>

<template>
  <div class="keyboard">
    <!-- ОТРИСОВКА РЯДОВ КЛАВЫ -->
    <div v-for="(row, rowIndex) in keyboardLayouts[currentLayout]" :key="rowIndex" class="keyboard-row">
      <!-- ОТРИСОВКА КЛАВИШ -->
      <div v-for="(item, itemIndex) in row" :key="itemIndex" @click="handleKeyPress(item)" class="key" :class="[specialKeys[item.keyValue],
      {
        'key-active': (item.keyValue === 'CapsLock' && props.capsLockEnabled) ||
          (item.keyValue === 'Shift' && props.shiftActive)
      }]">
        {{ displayedKeyValue(item) }} <!-- ОТОБРАЖЕНИЕ ЗНАЧЕНИЯ КЛАВИШ !-->
      </div>
    </div>
    <!-- КОМПОНЕНТ ДЛЯ ВЫБОРА РАСКЛАДКИ -->
    <KeyButtonLangs @changeLayout="changeLayout" />
    <KeyButtonDelete @deleteAll="hadleDeleteAll"/>
  </div>
</template>

<style>
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
