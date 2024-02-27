
<script setup>
import {defineProps} from 'vue';

const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expense:{
        type: Number,
        required: true
    }
})


</script>

<template>
    <div class="container">
        <div class="income">
            <h3>Income</h3>
            <h3 class="sum">${{ income }}</h3>
        </div>
        <div class="line"></div>
        <div class="expense">
            <h3>Expense</h3>
            <h3 class="sum">${{ expense }}</h3>

        </div>
    </div>
</template>


<style scoped>
.container{
    width: 282px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 10px 20px;
    background-color: white;
    box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
}
.income .sum{
    color:forestgreen;
}
.expense .sum{
    color: tomato;
}

.line{
    height: auto;
    width: 1px;
    background-color: lightgray;
}
h3{
    font-weight: 500;
}
</style>