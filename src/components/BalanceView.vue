<template>
    <h4>Seu Saldo</h4>
    <h1 id="balance">R$ {{ total.toFixed(2) }}</h1>
</template>

<script setup>
    import { defineProps } from 'vue';

    defineProps({
        total: {
            type: Number,
            required: true,
        }
    });
</script>