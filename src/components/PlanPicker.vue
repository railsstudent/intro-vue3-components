<script setup lang="ts">
import { Icon } from '@iconify/vue';
import { ref, computed } from 'vue';
import AddCoffeePlan from './AddCoffeePlan.vue';
import CoffeePlan from './CoffeePlan.vue';
const plans = ref(['The Single', 'The Curious', 'The Addict', 'The Hacker', 'Vibe Coder'])

const selectedPlan = ref('')
function handleSelectPlan(name: string) {
  selectedPlan.value = name
}

function isSelected(plan: string) {
  return selectedPlan.value === plan
}

const iconsNames = computed(() => {
		return selectedPlan.value.startsWith('The')  ? ['ic:outline-coffee', 'ic:outline-coffee-maker'] : [
			'ic:outline-emoji-food-beverage', 'ic:outline-fastfood'
		];
	});
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
      <template #coffee v-if="isSelected(plan) && plan.startsWith('The')">
        <div class="coffee">
          <Icon class="icon" v-for="icon in iconsNames" :key="icon" :icon="icon" />
        </div>
      </template>
  
      <template #beverage v-if="isSelected(plan) && !plan.startsWith('The')">
        <div class="beverage">
          <Icon class="icon" v-for="icon in iconsNames" :key="icon" :icon="icon" />
        </div>        
      </template>
    </CoffeePlan>
  </div>  
</template>

<style scoped>
.coffee {
  display: flex; 
  align-items: center;

  > .icon {
    width: 48px;
    height: 48px;
  }
}

.beverage {
  display: flex; 
  flex-direction: column; 
  padding: 0.25rem;

  > .icon {
    width: 42px;
    height: 42px;
    color: blue;
  }
}
</style>