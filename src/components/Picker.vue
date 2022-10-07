<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

defineProps<{ modelValue: number }>();

name: "number-picker";
const emit = defineEmits(["update:modelValue"]);

const emitValue = (e: Event & { target: HTMLInputElement } & { value: number}) => {
  emit("update:modelValue", parseInt(e.target.value));
};
</script>

<template>
  <input type="number" :value="modelValue" @input="emitValue" />
</template>

<style scoped></style>
