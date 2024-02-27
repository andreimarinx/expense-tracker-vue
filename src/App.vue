<script setup>
import { computed, onMounted, ref } from 'vue';
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue';
import History from './components/History.vue';
import AddTransaction from './components/AddTransaction.vue'
import { useToast } from 'vue-toastification';

const toast = useToast()

const transactions = ref([])

onMounted(()=>{
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
})

//Total Balance
const balance = computed(()=>{
  return transactions.value.reduce((acc, transation) => {
    return acc + transation.price
  }, 0)
})

//Total Income
const income = computed(()=>{
  return transactions.value.filter((transaction) => transaction.price > 0).reduce((acc, transation) => {
    return acc + transation.price
  }, 0)
})

//Total Expense
const expense = computed(()=>{
  return transactions.value.filter((transaction) => transaction.price < 0).reduce((acc, transation) => {
    return acc + transation.price
  }, 0)
})

//Submit Transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    title: transactionData.title,
    price: transactionData.price,
  });
  saveTransactionsToLocalStorage();

  toast.success('Transaction added.');
};

// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

//Remove Transaction
const removeTransaction =(id)=>{
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted.');
}

//Save transaction to storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};
</script>

<template>
  <main>
    <div class="container">
      <Header/>
      <Balance :balance="balance" />
      <IncomeExpense :income="income" :expense="expense" />
      <History :transactions="transactions" @removeTransaction="removeTransaction" />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
  
  </main>
</template>

<style>
main{
  box-sizing: border-box;
  font-family: "Open Sans";
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

h2{
  margin: 0;
}
h3{
  margin: 0;
}
h4{
  margin: 0;
}
p{
  margin: 0;
}
</style>
