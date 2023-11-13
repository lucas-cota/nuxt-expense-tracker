<template>
  <div>
    <h3>History</h3>
    <ul id="list" class="list">
      <li v-for="transaction in transactions" 
        :key="transaction.id"
      >
         {{ transaction.text }}
        <span> {{ transaction.amount }}</span>
        <button class="delete-btn">x</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
  const transactions = [
    {id:1, text: 'Flower', amount: -19.99},
    {id:2, text: 'Salary', amount: 299.97},
    {id:3, text: 'Book', amount: -10},
  ]
</script>