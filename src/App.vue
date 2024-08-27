<template>
  <AppHeader />
  <div>
    <BalanceView :total="+total"/>
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionHistory :transactions="transactions" @transaction-deleted="deleteTransaction" />
    <AddTransaction @transaction-added="addTransaction" />
  </div>
</template>

<script setup>
  import AppHeader from './components/AppHeader.vue'
  import BalanceView from './components/BalanceView.vue'
  import IncomeExpenses from './components/IncomeExpenses.vue'
  import TransactionHistory from './components/TransactionHistory.vue'
  import AddTransaction from './components/AddTransaction.vue'
  import { ref, computed, onMounted } from 'vue'
  import { useToast } from 'vue-toastification';

  const toast = useToast();
  const transactions = ref([]);

  onMounted(() => {
    const storedTransactions = JSON.parse(localStorage.getItem('transactions'));
    if (storedTransactions) {
      transactions.value = storedTransactions;
    }
  });
  

  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
  });

  const income = computed(() => {
    return transactions.value
      .filter((transaction) => transaction.amount > 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
  });

  const expenses = computed(() => {
    return transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
  });

  const addTransaction = (newTransaction) => {
    transactions.value.push(newTransaction);
    saveTransactions();
    toast.success('Transação adicionada com sucesso!');
  }

  const deleteTransaction = (id) => {
    transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
    saveTransactions();
    toast.success('Transação removida com sucesso!');
  }

  const saveTransactions = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  }
  
</script>