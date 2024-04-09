<template> 
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpense />
    <TransactionList :transactions ="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref } from 'vue';

const transactions = ref([
  { id: 1, text: "Food", amount: -20.00 },
  { id: 2, text: "Salary", amount: 320.00 },
  { id: 3, text: "Picnic", amount: -97.00 },
  { id: 4, text: "Books", amount: -50.00 },
  { id: 5, text: "Side gig", amount: 80.00 },
])
</script>