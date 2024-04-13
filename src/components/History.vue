<template>
  <div>
    <div>
      <h3>History</h3>
      <ul id="list" class="list">
        <li
          v-for="expenditure in expenditures"
          :key="expenditure.id"
          :class="expenditure.amount < 0 ? 'minus' : 'plus'"
        >
          {{ expenditure.text }} <span>#{{ expenditure.amount }}</span>
          <i
            @click="deleteTransaction(expenditure.id)"
            class="bi bi-trash-fill fs-5 me-3"
          ></i>
          <!-- <i @click="editTransaction(expenditure)" class="bi bi-pencil-square"></i> -->
          <a
            data-toggle="modal"
            data-target="#exampleModal"
            class="link-dark"
            @click="editTransaction(expenditure)"
            
            ><i class="bi bi-pencil-square fs-5 me-3"></i
          ></a>
        </li>
      </ul>
    </div> 
      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title"  id="exampleModalLabel">Edit Transaction</h5>
              <button type="button" class="md btn-close" data-dismiss="modal" aria-label="Close">&times;</button>
            </div>
            <div class="modal-body">
              <form @submit.prevent="saveChanges">
                <div class="mb-3">
                  <label for="editText" class="form-label">Text</label>
                  <input type="text"  v-model="editedTransaction.text"  class="form-control" id="editText">
                </div>
                <div class="mb-3">
                  <label for="editAmount" class="form-label">Amount</label>
                  <input type="number"  v-model="editedTransaction.amount"  class="form-control" id="editAmount">
                </div>
                <button type="submit" class="btn btn-primary">Save changes</button>
              </form>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { defineProps, defineEmits } from "vue";
const emit = defineEmits(["transactionDeleted", "editedTransaction"]);
const props = defineProps({
  expenditures: {
    type: Array,
    required: true,
  },
});

const editedTransaction = ref({ text: "", amount: 0 });


const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};

const editTransaction = (expenditure) => {
  emit("transactionEdited", expenditure);
}; 
const saveChanges = () => {
  emit("transactionEdited", editedTransaction.value);
}
</script>

<style scoped></style>
