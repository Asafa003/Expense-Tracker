<script setup>
import { ref, computed, onMounted } from "vue";
import Header from "./components/header.vue";
import Balance from "./components/Balance.vue";
import History from "./components/History.vue";
import AddTransactions from "./components/AddTransactions.vue";
import Transactions from "./components/Transactions.vue";


const expenditures = ref([]);

onMounted(() => {
   const savedTransactions = JSON.parse(localStorage.getItem('expenditures'));

   if (savedTransactions) {
    expenditures.value = savedTransactions;
   }
})

const total = computed(() => {
  return expenditures.value.reduce((acc, expenditure) => {
    return acc + expenditure.amount;
  }, 0)
})

const income = computed(() => {
  return expenditures.value
    .filter((expenditure) => expenditure.amount > 0)
    .reduce((acc, expenditure) => {
      return acc + expenditure.amount;
    }, 0)
});

const expenses = computed(() => {
  return expenditures.value
    .filter((expenditure) => expenditure.amount < 0)
    .reduce((acc, expenditure) => {
      return acc + expenditure.amount;
    }, 0)
});

const handleTransaction = (transactionDetails) => {
  expenditures.value.push(
    {
      id:Math.floor(Math.random() * 1000000),
      text:transactionDetails.text,
      amount:transactionDetails.amount
    }
  )

  savedData();
}

const handleDelete = (id) => {
  expenditures.value  = expenditures.value.filter((expenditure) => expenditure.id !==id);

  savedData();
}

const handleEdit = (editedTransaction) => {
  const index = expenditures.value.findIndex((expenditure) => expenditure.id === editedTransaction.id);
  if (index !== -1) {
    expenditures.value[index] = editedTransaction;
    savedData();
  }
}




const savedData = () => {
  localStorage.setItem('expenditures', JSON.stringify(expenditures.value))
}

</script>

<template>
  <div>
    <Header />
    <Balance :total="total" />
    <Transactions :income="income" :expenses="expenses" />
    <History :expenditures="expenditures" @transactionDeleted ="handleDelete" @editedTransaction="handleEdit"/>
    <AddTransactions @transactionSubmit="handleTransaction" />
  </div>
</template>

<style scoped></style>
