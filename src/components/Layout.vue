<script setup>

  import Gerador from './Gerador.vue'

  const props = defineProps({
      msg: String,
    });


</script>

<template>
  
  <div class="h-screen w-screen flex flex-col justify-center items-center space-y-8">
    
    <div class="block text-center text-2xl bg-red-500-100 uppercase">
      <span class="text-slate-600">{{ msg }}</span>
    </div>
    <div>
      <Gerador />
    </div>
  </div>

  
</template>

<style scoped>

</style>
