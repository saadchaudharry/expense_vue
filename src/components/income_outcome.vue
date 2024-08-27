<template>
    <div class="row">
        <div class="col-6">
            <h2>INCOME</h2>
            <p class="income">${{ income }}</p>
        </div>
        <div class="col-6">
            <h2>EXPENSE</h2>
            <p class="expense">${{ expense }}</p>
        </div>
    </div>
    <hr>
</template>


<script setup>

import {defineProps} from 'vue'

const props = defineProps({
    income:{
        type:Number,
        required:true
    },
    expense:{
        type:Number,
        required:true
    }

})


</script>

