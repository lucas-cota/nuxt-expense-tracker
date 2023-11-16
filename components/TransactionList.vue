<template>
  <div>
    <h3>History</h3>
    <ul id="list" class="list">
      <li 
        v-for="transaction in transactions" 
        :key="transaction.id"
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
      >
         {{ transaction.text }}
        <span>$ {{ transaction.amount }}</span>
        <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
interface Transactions {
  id:number,
  text: string,
  amount: number
}

const emit = defineEmits(['transactionDeleted'])

defineProps({
  transactions: {
    type: Array as() => Array<Transactions>,
    required: true
  } 
})

const deleteTransaction = (id:number) => {
  emit('transactionDeleted', id)
}
</script>