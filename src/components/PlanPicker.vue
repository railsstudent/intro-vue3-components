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
      <template #icon="{ iconsNames }" v-if="isSelected(plan)">
        <div>
          <Icon v-for="icon in iconsNames" :key="icon" :icon="icon" width="48" height="48" />
        </div>        
      </template>
    </CoffeePlan>
  </div>  
</template>
