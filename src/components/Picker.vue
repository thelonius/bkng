<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

defineProps<{ modelValue: number }>();

name: "number-picker";
const emit = defineEmits(["update:modelValue"]);

const emitValue = (
  e: Event & { target: HTMLInputElement } & { value: number }
) => {
  const value = parseInt(e.target.value);
  if (value) {
    emit("update:modelValue", value);
  }
};
</script>

<template>
  <input type="number" :value="modelValue" @change="emitValue" />
</template>

<style scoped></style>
