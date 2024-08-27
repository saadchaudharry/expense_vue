<template>
    <ul class="transaction-history">
        <li 
            v-for=" transaction in  transactions "
            :key="transaction.id"
            :class="transaction.amount < 0 ? 'expense' : 'income'" >
            <span class="text">{{ transaction.expense_title }}</span>
            <span class="amount">{{ transaction.amount }}</span>
            <button 
                class="remove-btn"
                @click="deleteTransaction(transaction.id)"
            >Remove</button>

        </li>

    </ul>
</template>


<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});


const emit = defineEmits(['deleteTransaction_row'])


const deleteTransaction = (id) =>{
    console.log(id)

    emit('deleteTransaction_row',id)

    
}





</script>
