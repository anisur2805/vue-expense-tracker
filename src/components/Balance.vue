<template>
  <div class="balance">
    Your Balance
    <div class="amount">${{ total }}</div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  total: {
    type: Number,
    required: true
  }
})
</script>
