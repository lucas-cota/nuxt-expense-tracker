<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpenses :income="+income" :expenses="+expenses"/>
      <TransactionList :transactions="transactions" @transaction-deleted="handleTransactionDeleted"/>
      <AddTransactions @transaction-submitted="handleTransactionSubmitted" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { useToast } from 'vue-toastification';

interface Transaction {
  id:number,
  text: string,
  amount: number
}

const toast = useToast();

const transactions = ref<Array<Transaction>>([]);

onMounted(() => {
  const savedTransactions = localStorage.getItem('transactions');

  if(savedTransactions){
    transactions.value = JSON.parse(savedTransactions)
  }
})

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
  });

  savedTransactionsToLocalStorage();

  toast.success('Transaction added');
};


//generate unique id
const generateUniqueId = () => {
  return Math.floor(100000000 + Math.random() * 900000000);
};

//delete transaction
const handleTransactionDeleted = (id:number) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  savedTransactionsToLocalStorage();

  toast.success('Transaction deleted')
};

//save to localStorage
const savedTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>
