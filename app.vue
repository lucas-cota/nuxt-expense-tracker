<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpenses :income="+income" :expenses="+expenses"/>
      <TransactionList :transactions="transactions" />
      <AddTransactions @transaction-submitted="handleTransactionSubmitted" />
    </div>
  </div>
</template>

<script setup lang="ts">

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10 },
]);

//get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
}); 

//get income
const income = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount > 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
}); 

//get expense
const expenses = computed(() => {
  return transactions.value
  .filter((transaction) => transaction.amount < 0)
  .reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
}); 

//add transaction
const handleTransactionSubmitted = (transactionData:{text:string, amount:number}) => {
  transactions.value.push({
    id:generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
}


//generate unique id
const generateUniqueId = () => {
  return Math.floor(Math.random() + 100000)
}

</script>
