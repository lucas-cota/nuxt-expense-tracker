<template>
  <div>
    <h4>Your Balance</h4>
    <h1 id="balance">${{ total }}</h1>
  </div>
</template>

<script lang="ts" setup>
defineProps({
  total: {
    type: Number,
    required: true
  }
})
</script>


