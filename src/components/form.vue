<template>
    <div class="new-transaction">
        <form id="form" @submit.prevent="onSubmit">
            <h2>Add new transaction</h2>
            <input type="text" v-model="text"  placeholder="Text">
            <input type="number" v-model="number" placeholder="Amount (negative - expense, positive - income)">
            <button>Add transaction</button>
        </form>
    </div>
</template>


<script setup>
import {ref} from 'vue';

const text   = ref('')
const number = ref('')

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
    console.log(text.value)
    console.log(number.value)


    const transactionData = {
        text: text.value,
        number: parseFloat(number.value),
    }

    emit('transactionSubmitted', transactionData);

    // Clear form fields
    text.value = '';
    number.value = '';

}

</script>


