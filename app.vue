<template>
  <div>
    <Header />
    <div class="container">
      <Balance />
      <IncomeExpenses />
      <TransactionList :transactions="transactions"/>
      <AddTransactions />
    </div>
  </div>
</template>

<script setup lang="ts">

  const transactions = ref([
    {id:1, text: 'Flower', amount: -19.99},
    {id:2, text: 'Salary', amount: 299.97},
    {id:3, text: 'Book', amount: -10},
  ])
</script>
