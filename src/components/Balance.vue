
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    balance:{
        type: Number,
        required: true
    }
})
</script>

<template>
    <div class="container">
        <h3>Your Balance</h3>
         <h2>${{ balance }}</h2>
    </div>
  

</template>

<style scoped>
.container{
    margin: 10px 0px;
    padding: 0;
}
h2{
    font-weight: 500;
}
</style>