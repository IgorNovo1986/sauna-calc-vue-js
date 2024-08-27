<template>
  <div class="bg-white p-6 rounded-lg shadow-lg max-w-md w-full">
    <h1 class="text-2xl font-bold mb-4 text-center text-black">Сауна калькулятор прайс vue</h1>

    <div class="mb-4">
      <label for="people" class="block text-sm font-medium text-gray-700">Яка кількість людей планується?</label>
      <select v-model="people" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 cursor-pointer">
        <option v-for="index in 4" :key="index" :value="index">{{ index }}</option>
      </select>
    </div>

    <div class="mb-4">
      <label for="hours" class="block text-sm font-medium text-gray-700">Скільки годин ?</label>
      <select v-model="hours" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 cursor-pointer">
        <option v-for="index in 3" :key="index" :value="index">{{ index }}</option>
      </select>
    </div>

    <div class="mb-4">
      <label for="day" class="block text-sm font-medium text-gray-700">Який день тижня?</label>
      <select v-model="day" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 cursor-pointer">
        <option v-for="dayOfTheWeek in week" :key="dayOfTheWeek.value" :value="dayOfTheWeek.value">{{ dayOfTheWeek.title }}</option>
      </select>
    </div>

    <div class="mb-6">
      <label for="sauna" class="block text-sm font-medium text-gray-700">Який номер сауни?</label>
      <select v-model="saunaId" class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 cursor-pointer">
        <option v-for="sauna in saunas" :key="sauna.id" :value="sauna.id">{{ sauna.name }}</option>
      </select>
    </div>

    <button
        @click="calculateCost"
        class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 my-6"
    >
      Підрахувати
    </button>

    <div class="mt-6">
      <h2 class="text-xl font-bold my-6 pb-6 border-b-2 border-gray-700">До оплати:</h2>
      <p class="text-gray-700 my-2 flex justify-between">Загальна вартість: <span v-if="totalCost !== null" class="font-bold text-black uppercase">{{ totalCost }} грн</span></p>
      <p class="text-gray-700 my-2 flex justify-between">Вартість з особи: <span v-if="totalCost !== null" class="font-bold text-black uppercase">{{ costPerPerson }} грн</span></p>
    </div>
  </div>
</template>

<script setup>

import { saunasData, daysData } from "@/data";

import { ref } from 'vue';

const people = ref(1);
const hours = ref(1);
const day = ref('monday');
const week = ref(daysData)
const saunaId = ref(1);
const totalCost = ref(null);
const costPerPerson = ref(null);

const saunas = ref(saunasData)

const calculateCost = () => {
  const selectedSauna = saunas.value.find(sauna => sauna.id === saunaId.value);
  let baseCost;

  switch (hours.value) {
    case 1:
      baseCost = selectedSauna.one_hour[day.value];
      break;
    case 2:
      baseCost = selectedSauna.two_hours[day.value];
      break;
    case 3:
      baseCost = selectedSauna.three_hours[day.value];
      break;
  }

  totalCost.value = baseCost;
  costPerPerson.value = baseCost / people.value;
};
</script>
