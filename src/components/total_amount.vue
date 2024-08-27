<template>
    <h1>Expense Tracker</h1>
    <h2 class="balance">${{ totalamount }}</h2>
    <hr>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    totalamount: {
        type: Number,
        required: true,
    },
})



</script>
