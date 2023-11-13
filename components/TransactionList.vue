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
        <button class="delete-btn">x</button>
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
  
  defineProps({
    transactions: 
      {
        type: Array as() => Array<Transactions>,
        required: true
      } 
 })
</script>