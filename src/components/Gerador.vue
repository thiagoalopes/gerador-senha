<script setup>

import { reactive } from 'vue';  

let configuration = reactive({
  tamanho:5,
  alfabetico:true,
  numerico:true,
  especial:false,
  senha: ''
});

let especialCharCode = [21,23,24,26,42,47,58,63,64,94,95];

let alfabeticoCharCode = [41, 42, 43, 44, 45, 46, 47, 48,
  49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 
  63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76,
  77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90,
  91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103,
  104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114,
  115, 116, 117, 118, 119, 120, 121, 122];

let numericoCharCode = [48,49,50,51,52,53,54,55,56,57];

function gerarListaDeCaracteres() {

  let caracteresDisponiveis = [];

  if(configuration.alfabetico) {
    caracteresDisponiveis = caracteresDisponiveis.concat(alfabeticoCharCode);
  } else if(configuration.numerico){
    caracteresDisponiveis = caracteresDisponiveis.concat(numericoCharCode);
  }else if(configuration.especial){
    caracteresDisponiveis = caracteresDisponiveis.concat(especialCharCode);
  }
  return caracteresDisponiveis;
}

function gerarSenha(){

  let listaCaracteresSelecionados = gerarListaDeCaracteres();
  let senha = '';

  for (let index = 0; index < configuration.tamanho; index++) {
    const indice = Math.floor(Math.random() * listaCaracteresSelecionados.length);
    senha += listaCaracteresSelecionados[indice];
  }
  configuration.senha = senha;
}

</script>

<template>
  <div class="space-y-4 flex flex-col items-center">
    <input :value="configuration.senha" type="text" disabled class="block border-2 border-blue-200 p-2 rounded-lg focus:outline-none focus:border-blue-300 w-96">
    <button @click="gerarSenha" class="block border-2 border-green-400 p-2 rounded-lg bg-green-400 hover:bg-green-600 font-bold hover:border-green-600 text-white w-24">Gerar</button>
    <div class="flex justify-center pb-2 w-full">
      <input type="range" v-model="configuration.tamanho" min="5" max="32" id="slider">
      <span class="ml-2 text-slate-400 text-xl">{{ configuration.tamanho }}</span>
    </div>
    <div class="flex justify-start w-full">
      <input id="alfabetico" class="border border-blue-500 rounded cursor-pointer w-6 p-6" v-model="configuration.alfabetico" :checked="configuration.alfabetico" type="checkbox">
        <label class="text-slate-400 text-xl ml-4" for="alfabetico">[a-zA-Z]</label>
    </div>
    <div class="flex justify-start w-full">
      <input id="numerico" class="border border-blue-500 rounded cursor-pointer w-6 p-6" v-model="configuration.numerico" :checked="configuration.numerico" type="checkbox">
        <label class="text-slate-400 text-xl ml-4" for="numerico">[0-9]</label>
    </div>
    <div class="flex justify-start w-full">
      <input id="especial" class="border border-blue-500 rounded cursor-pointer w-6 p-6" v-model="configuration.especial" :checked="configuration.especial" type="checkbox">
        <label class="text-slate-400 text-xl ml-4" for="especial">[@./-&]</label>
    </div>
</div>
  
</template>

<style scoped>

</style>
