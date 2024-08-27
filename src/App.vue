<template>
    <div class="container">
        <total_amountVue :totalamount="get_total" />
        <income_outcomeVue :income="+income" :expense="+expenses" />
        <transactionVue :transactions="data" @deleteTransaction_row="delete_data" />
        <formVue @transactionSubmitted="handleTransactionSubmitted" />

    </div>
</template>

<script setup>
import total_amountVue from "./components/total_amount.vue";
import income_outcomeVue from "./components/income_outcome.vue";
import transactionVue from "./components/transaction.vue"
import formVue from "./components/form.vue"



import { ref, computed, onMounted } from 'vue';

const data =ref([]);




onMounted(() => {
    console.log('www')

    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if (savedTransactions) {
        data.value = savedTransactions;
    }

})




const get_total = computed(() => {
    return data.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0);
});

// Get income
const income = computed(() => {
  return data.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// Get expenses
const expenses = computed(() => {
  return data.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// Submit transaction
const handleTransactionSubmitted = (transactionData) => {
  data.value.push({
    id: generateUniqueId(),
    expense_title: transactionData.text,
    amount: transactionData.number,
  });
  saveTransactionsToLocalStorage();


};


// Submit transaction
const delete_data = (id) => {
    console.log(`${id}wwww`)
    data.value = data.value.filter( i => i.id !== id  )
    saveTransactionsToLocalStorage();

};


// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(data.value));
};
</script>
