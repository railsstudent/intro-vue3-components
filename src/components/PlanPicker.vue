<script setup lang="ts">
import { ref } from 'vue'
import CoffeePlan from './CoffeePlan.vue'
const plans = ref(['The Single', 'The Curious', 'The Addict', 'The Hacker'])

const selectedPlan = ref('')
function handleSelectPlan(name: string) {
  selectedPlan.value = name
}

const newPlan = ref('');
function addPlan() {
  if (!newPlan.value) {
    return;
  }

  plans.value.push(newPlan.value);
  newPlan.value = '';
} 
</script>

<template>
  <div class="plans">
    <form class="add-plan-form" @submit.prevent="addPlan">
      <input v-model.trim="newPlan" type="text" placeholder="Add a new plan" />
      <button class="btn btn-primary" type="submit" :disabled="newPlan.length < 5">
        Add Plan
      </button>
    </form>
    {{ selectedPlan }}
    <CoffeePlan
      v-for="plan in plans"
      :key="plan"
      :name="plan"
      :selected="selectedPlan == plan"
      @selectedPlan="handleSelectPlan"
    />
  </div>
</template>

<style scoped>
input {
  padding: 0.5rem 0.75rem;
}

.add-plan-form {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.add-plan-form input {
  width: 70%;
  border-radius: 3px;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  border: 1px solid #f1f5f8;
  color: #606f7b;
  padding: 0.5rem 0.75rem;
  box-sizing: border-box;
  font-size: 1rem;
  letter-spacing: 0.5px;
  margin: 0.5rem 0;
}
</style>