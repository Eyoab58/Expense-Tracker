<template>
  <Header />
  <div class="container">
    <Balance :total="total"/>
    <IncomeExpense :income="+income" :expenses="+expenses"/>
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />

  </div>
</template>


<script setup>
 import Header from './components/Header.vue';
 import Balance from './components/Balance.vue'; 
 import IncomeExpense from './components/IncomeExpenses.vue';
 import TransactionList from './components/TransactionList.vue';
 import AddTransaction from './components/AddTransaction.vue';  

import { useToast } from 'vue-toastification'

 import {ref, computed, onMounted } from 'vue';

    const toast = useToast();

    onMounted(() => {
      const savedTransaction = JSON.parse(localStorage.getItem('transactions'));

      if(savedTransaction){
        transactions.value = savedTransaction
      }
    })


    const transactions = ref([]);

    //Get total
    const total = computed(() => {
      return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0);
    });

    //Get income
      const income = computed(() => {
      return transactions.value.filter((transactions)=> transactions.amount > 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0);
    });

    //Get expenses
      const expenses = computed(() => {
      return transactions.value.filter((transactions)=> transactions.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0)
      .toFixed(2);
    });


//Add transaction

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionToLocalStorage();
  toast.success('Transaction added');
}

//Delete transaction

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) =>transaction.id !== id);

    saveTransactionToLocalStorage();
    toast.success('Transaction Deleted');
}

//Save to localstorage

const saveTransactionToLocalStorage = () =>{
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000);
}
</script>