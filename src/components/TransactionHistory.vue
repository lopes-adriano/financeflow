<template>
    <h3>Histórico</h3>
    <ul id="list" class="list">
      <li
        v-for="transaction in transactions"
        :key="transaction.id"
        :class="transaction.amount < 0 ? 'minus' : 'plus'"
      >
        {{ transaction.text }} <span>{{ transaction.amount < 0 ? '-R$' : 'R$' }} {{ Math.abs(transaction.amount) }}</span>
        <button class="delete-btn" @click="deleteTransaction(transaction.id)">
          x
        </button>
      </li>
    </ul>
  </template>

<script setup>
    import { defineProps } from 'vue';

    const emit = defineEmits(['transaction-deleted']);

    defineProps({
        transactions: {
            type: Array,
            required: true,
        }
    });

    const deleteTransaction = (id) => {
        emit('transaction-deleted', id);
    }


</script>
