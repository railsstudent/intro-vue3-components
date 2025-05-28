<script setup lang="ts">
import { ref } from 'vue'
import CoffeePlan from './CoffeePlan.vue'
import AddCoffeePlan from './AddCoffeePlan.vue'
const plans = ref(['The Single', 'The Curious', 'The Addict', 'The Hacker'])

const selectedPlan = ref('')
function handleSelectPlan(name: string) {
  selectedPlan.value = name
}
</script>

<template>
  <div class="plans">
    <AddCoffeePlan @newCoffeePlan="(plan) => plans.push(plan)" />
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
