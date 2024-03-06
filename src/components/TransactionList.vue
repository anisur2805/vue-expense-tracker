<template>
  <div class="traction-list">
    <h3>History</h3>
    <ul>
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        class="transaction"
        :class="{ plus: transaction.amount > 0, minus: transaction.amount < 0 }"
      >
        {{ transaction.text }}
        <span>{{ transaction.amount }}</span>
        <button @click="deleteTransaction(transaction.id)">&#xD7;</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

const emits = defineEmits(['deleteTransaction'])

const deleteTransaction = (id) => {
  emits('deleteTransaction', id)
}
</script>
