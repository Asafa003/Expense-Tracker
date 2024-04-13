<template>
  <div>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div 
      >
      <label for="text">Text</label>
      <input
      type="text"
      class="form-control"
          id="text"
          v-model="text"
          placeholder="Enter text..."
        />
      </div>
      <div 
      >
      <label for="amount">Amount <br /> </label>
      <input
      type="number"
      class="form-control"
          id="amount"
          v-model="amount"
          placeholder="Enter amount..."
        />
      </div>
      <button class="btn">Add transaction</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(['transactionSubmit', 'transactionEdited']);
const text = ref("");
const amount = ref("");
const onSubmit = () => {
  if (!text.value || !amount.value) {
    alert("Fields empty");
    return;
  }

  const transactionDetails = {
    text: text.value,
    amount: amount.value,
  };
  
  emit('transactionSubmit', transactionDetails);

  (text.value = ""), (amount.value = "");
};
// (text.value = ""), (amount.value = 0);
</script>

<style scoped></style>
