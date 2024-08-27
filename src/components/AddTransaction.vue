<template>
    <h3>Adicionar nova transação</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="text">Descrição</label>
        <input type="text" id="text" placeholder="Ex: Compra de roupas" v-model="text" />
      </div>
      <div class="form-control">
        <label for="amount"
          >Valor <br />
          (negativo - despesa, positivo - entrada)</label
        >
        <input
          type="text"
          id="amount"
          placeholder="Digite o valor..."
          v-model="amount"
        />
      </div>
      <button class="btn">ADICIONAR</button>
    </form>
  </template>

<script setup>

  import { ref } from 'vue';
  import { useToast } from 'vue-toastification';

  const text = ref('');
  const amount = ref('');
  const emit = defineEmits(['transaction-added']);

  const toast = useToast();
  
  const onSubmit = () => {
    if (text.value.trim() === '' || amount.value.trim() === '') {
      toast.error('Por favor, adicione a descrição e o valor da transação');
      return;
    }

    const newTransaction = {
      id: Date.now() + Math.random() * 100000,
      text: text.value,
      amount: parseFloat(amount.value),
    }

    emit('transaction-added', newTransaction);

    // clean form
    text.value = '';
    amount.value = '';
    document.getElementById('form').reset();
  }
</script>
