<script setup lang="ts">
import { ref } from 'vue'
import CoffeePlan from './CoffeePlan.vue'
import AddCoffeePlan from './AddCoffeePlan.vue'
const plans = ref(['The Single', 'The Curious', 'The Addict', 'The Hacker'])

const selectedPlan = ref('')
function handleSelectPlan(name: string) {
  selectedPlan.value = name
}

function addPlan(newPlan: string) {
  plans.value.push(newPlan);
} 
</script>

<template>
  <div class="plans">
    <AddCoffeePlan @newCoffeePlan="addPlan" />
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
