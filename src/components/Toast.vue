<template>
  <div v-if="show" class="toast" :style="`top: ${position.top}px; left: ${position.left}px;`">
    Copiado com sucesso
  </div>
</template>

<script setup>

import { reactive, ref, defineProps, onMounted } from 'vue';

const props = defineProps({
  y: Number,
  x: Number,
});

const show = ref(false);
let position = reactive({ top: 0, left: 0 });

console.log(props.y);
const showToast = () => {
  const x = props.x;
  const y = props.y;
  const toastWidth = 120; // largura estimada do toast
  const toastHeight = 40; // altura estimada do toast
  const margin = 10; // margem entre o cursor e o toast

  position = {
    top: y - toastHeight - margin,
    left: x + margin // Ajuste para o toast ficar à direita do cursor
  };
  show.value = true;
  setTimeout(() => {
    show.value = false;
  }, 30000); // 2 segundos
};

onMounted(() => {
  document.addEventListener('copy', showToast);
});

</script>

<style>
.toast {
  position: fixed;
  background-color: #333;
  color: white;
  padding: 8px 16px;
  border-radius: 4px;
  z-index: 9999;
}
</style>
