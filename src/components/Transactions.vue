<template>
  <div>
    <div class="container">
      <div class="inc-exp-container">
        <div>
          <h4>Income</h4>
          <p id="money-plus" class="money plus">
            #{{ income }}
          </p>
        </div>
        <div>
          <h4>Expense</h4>
          <p id="money-minus" class="money minus">
            #{{ expenses }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
const props = defineProps({
  income: {
    type: Array,
    required: true,
  },
  expenses: {
    type: Array,
    required: true,
  }
});
</script>

<style scoped></style>
