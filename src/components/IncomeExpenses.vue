<template>
    <div class="inc-exp-container">
      <div>
        <h4>Entradas</h4>
        <p id="money-plus" class="money plus">+R$ {{ income }}</p>
      </div>
      <div>
        <h4>Saídas</h4>
        <p id="money-minus" class="money minus">-R$ {{ Math.abs(expenses) }}</p>
      </div>
    </div>
  </template>

<script setup>
    import { defineProps } from 'vue';

    defineProps({
        income: {
            type: Number,
            required: true,
        },
        expenses: {
            type: Number,
            required: true,
        }
    });
</script>