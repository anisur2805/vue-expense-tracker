<template>
  <div class="inc-exp-container">
    <div>
      Income
      <div class="text-green">+${{ income }}</div>
    </div>
    <div>
      Expenses
      <div class="text-red">${{ expense }}</div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  income: {
    type: Number,
    required: true
  },
  expense: {
    type: Number,
    required: true
  }
})
</script>
