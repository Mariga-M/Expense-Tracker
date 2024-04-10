<template> 
  <Header />
  <div class="container">
    <Balance :total="+total"/>
    <IncomeExpense :income="+income" :expense="+expense"/>
    <TransactionList 
      :transactions ="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import {useToast} from 'vue-toastification'

import { ref, computed, onMounted } from 'vue';

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTrasactions = JSON.parse(localStorage.getItem('transactions'))

  if(savedTrasactions){
    transactions.value = savedTrasactions;
  }
})

// get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction)=> {
    return acc + transaction.amount
  }, 0)
  .toFixed(2);
})

// get income
const income = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount > 0)
  .reduce((acc, transaction)=> {
    return acc + transaction.amount;
  }, 0)
  .toFixed(2);
})

//get expenses
const expense = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount < 0)
  .reduce((acc, transaction)=> {
    return acc + transaction.amount;
  }, 0)
  .toFixed(2);
})

//add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTrasactionsToLocalStorage()

  toast.success('Transaction added')
}

//generate id
const generateUniqueId = () => {
 return Math.floor(Math.random() * 10000);
}

//delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id != id)

  saveTrasactionsToLocalStorage()

  toast.success('Transaction deleted')
}

//save to localstorage
const saveTrasactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

</script>