<template>
  <Header />
  <Balance :total="+total" />
  <IncomeExpense v-if="transactions.length" :income="+income" :expense="+expense" />
  <TransactionList v-if="transactions.length" @deleteTransaction="deleteTransaction" :transactions="transactions" />
  <AddTransaction @addTransaction="addTransaction" />
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

import AddTransaction from './components/AddTransaction.vue'
import Balance from './components/Balance.vue'
import Header from './components/Header.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'

import { useToast } from 'vue-toastification'

const toast = useToast()

const transactions = ref([])

// Total amount
const total = computed(() => {
  return transactions.value.reduce((acc, curr) => (acc += curr.amount), 0).toFixed(2)
})

onMounted(() => {
  const saveTransactions = JSON.parse(localStorage.getItem('transactions'))

  if (saveTransactions) {
    transactions.value = saveTransactions
  }
})
// Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => (acc += transaction.amount), 0)
    .toFixed(2)
})

// Expense
const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => (acc += transaction.amount), 0)
    .toFixed(2)
})

// Add transaction to main transaction
const addTransaction = (transaction) => {
  console.log({ transaction })
  transactions.value.push({
    id: generateUID(),
    text: transaction.text,
    amount: transaction.amount
  })
 
  saveTransactions();

  toast.success('Transaction added.')

  console.log(transactions.value)
}

// Generate Uid
const generateUID = () => {
  return Math.floor(Math.random() * 100000)
}

// Delete Transaction
const deleteTransaction = (id) => {
  console.log(id)
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
  
  saveTransactions()

  toast.success('Transaction deleted successfully.')
}

// Save transaction in LocalStorage
const saveTransactions = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>

<style scoped></style>
