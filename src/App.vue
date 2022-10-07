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

const finish = ref(new Date(today.setDate(today.getDate() + 1)));
const duration = ref(10);

const doIt = () => console.log(start);

const updateFinish = (days: number) =>
  (finish.value = new Date(finish.value.setDate(today.getDate() + days)));

watch(duration, (next, prev) => {
  updateFinish(next);
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

  <datepicker v-model="start" />
  <number-picker v-model="duration" />
  <div>
    <button @click="duration++">+</button>
    <span>{{ duration }}</span>
    <button @click="duration--">-</button>
    <button @click="doIt">do it</button>
  </div>
  <datepicker v-model="finish" />
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
