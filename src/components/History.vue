<script setup>
import {ref, defineProps} from 'vue';

const emit = defineEmits(['removeTransaction'])

const props = defineProps({
    transactions:{
        type: Array,
        required: true
    }
})

const removeTransaction =(id)=>{
    emit('removeTransaction', id)
}

</script>

<template>
    <div class="container">
        <h3>History</h3>
        <div class="line"></div>
        <ul class="transactions">
            <li v-for="transaction in transactions" class="transaction" :key="transaction.id">

                <h4>{{ transaction.title }}</h4>
                <div class="total">
                    <p>${{ transaction.price }}</p>
                    <div :class="transaction.price<0? 'type neg' : 'type pos'" />
                </div>
                <button @click="removeTransaction(transaction.id)" class="remove">x</button>

            </li>
        </ul>

    </div>
</template>

<style scoped>
    ul{
        list-style: none;
        padding: 0;
    }
    .container{
        margin: 20px 0;
    }
    .line{
        margin: 10px 0;
        height: 1px;
        width: auto;
        background-color: lightgray;
    }
    
    .transaction{
        box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
        width: auto;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-left: 10px;
        margin: 10px 0;
        position: relative;

    }
    .total{
        display: flex;
        align-items: center;
    }
    .type{
        width: 5px;
        height: 30px;
        margin-left: 10px;
    }
    .type.pos{
        background-color: forestgreen;
    }
    .type.neg{
        background-color: tomato;
    }
    .transaction h4{
        font-weight: 500;
        
    }
   .remove{
    cursor: pointer;
    border-radius: 50%;
    background-color: tomato;
    border: 0;
    position: absolute;
    left: 100px;
    left: -30px;
    color: white;
    line-height: 20px;
    padding: 1px 8px;
    opacity: 0;
  opacity: 0;
  transition: opacity 0.2s ease;
   }

   .transaction:hover .remove{
    opacity: 1;
   }
</style>