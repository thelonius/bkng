<script setup lang="ts">
import Datepicker from "vue3-datepicker";
import NumberPicker from "./components/Picker.vue";
import { ref, defineProps, onMounted, watch } from "vue";
export interface Props {
  initValue?: number;
}
const props = withDefaults(defineProps<Props>(), {
  initValue: 7,
});
const today = new Date();
const months = [
  "января",
  "февраля",
  "марта",
  "апреля",
  "мая",
  "июня",
  "июля",
  "августа",
  "сентября",
  "октября",
  "ноября",
  "декабря",
];
const start = ref(today);

const finish = ref(new Date(today.setDate(today.getDate())));
const duration = ref(10);

const updateFinish = (days: number) => {
  finish.value = new Date(new Date().setDate(new Date().getDate() + days));
  updateDuration(days);
};

const updateDuration = (days: number) => {
  // duration.value = days;
  // console.log(days)
};

watch(duration, (next) => {
  updateFinish(next);
});
watch(finish, (next) => {
  const diff = next.getTime() - today.getTime();
  const days = Math.ceil(diff / (1000 * 3600 * 24));
  updateDuration(days);
});

onMounted(() => {
  duration.value = props.initValue;
});
</script>

<template>
  <div>
    {{ today }}
  </div>
  <span
    >You spend {{ duration }} days from
    {{ `${start.getDate()} ${months[start.getMonth()]}` }} to
    {{ `${finish.getDate()} ${months[finish.getMonth()]}` }}</span
  >

  <datepicker inputFormat="dd.MM.yyyy" v-model="start" />
  <number-picker v-model="duration" />
  <div>
    <button @click="duration++">+</button>
    <span>{{ duration }}</span>
    <button @click="duration--">-</button>
    <button @click="doIt">do it</button>
  </div>
  <datepicker inputFormat="dd.MM.yyyy" v-model="finish" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
