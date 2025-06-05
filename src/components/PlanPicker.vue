<script setup lang="ts">
import { Icon } from '@iconify/vue';
import { ref } from 'vue';
import AddCoffeePlan from './AddCoffeePlan.vue';
import CoffeePlan from './CoffeePlan.vue';
const plans = ref(['The Single', 'The Curious', 'The Addict', 'The Hacker'])

const selectedPlan = ref('')
function handleSelectPlan(name: string) {
  selectedPlan.value = name
}

function isSelected(plan: string) {
  return selectedPlan.value === plan
}
</script>

<template>
  <div class="plans">
    <AddCoffeePlan @newCoffeePlan="(plan) => plans.push(plan)">
      <template #btn="{ hover }">
        Add Plan  {{ hover ? '(+1)' : '' }}
      </template>
    </AddCoffeePlan>
    {{ selectedPlan }}
    <CoffeePlan
      v-for="plan in plans"
      :key="plan"
      :name="plan"
      :selected="isSelected(plan)"
      @selectedPlan="handleSelectPlan"
    >
      <template #icon v-if="isSelected(plan)">
        <Icon icon="material-symbols:coffee-maker-outline" width="48" height="48" />
        <Icon icon="material-symbols:coffee-outline" width="48" height="48" />
      </template>
    </CoffeePlan>

  </div>  
</template>
