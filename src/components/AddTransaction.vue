<script setup>
import {ref} from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast()

const amount = ref('');
const  name = ref('')

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = ()=>{
  if(!amount.value || !name.value){
    toast.error("Both fields have to be filled!")
    return
  }


  const transactionData = {
    title: text.value,
    price: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);


  name.value = '';
  amount.value = '';
}
</script>

<template>

<div class="container">
        <h3>Add Transaction</h3>
        <div class="line"></div>

        <form id="form" @submit.prevent="onSubmit">
            <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="name" placeholder="Enter text..." />
            </div>
            <div class="form-control">
            <label for="amount"
                >Amount <br />
                (negative - expense, positive - income)</label
            >
            <input
                type="text"
                id="amount"
                v-model="amount"
                placeholder="Enter amount..."
             
            />
            </div>
            <button class="btn">Add transaction</button>
        </form>
      </div>
</template>

<style scoped>
 .container{
        margin: 20px 0;
    }
    .line{
        margin: 10px 0;
        height: 1px;
        width: auto;
        background-color: lightgray;
    }
    label {
  display: inline-block;
  margin: 10px 0;
}

input[type='text'],
input[type='number'] {
  border: 1px solid #dedede;
  border-radius: 5px;
  display: block;
  font-size: 16px;
  padding: 10px 10px;
width:300px;
}

.btn {
  cursor: pointer;
  background-color:coral;
  box-shadow: var(--box-shadow);
  color: #fff;
  border: 0;
  display: block;
  font-size: 16px;
  margin: 10px 0 30px;
  padding: 10px;
  width: 100%;
  border-radius: 5px;
}

.btn:focus,
.delete-btn:focus {
  outline: 0;
}
    
</style>