<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits<{
  (e: 'newCoffeePlan', name: string): void
}>();

const hover = ref(false);

const newPlan = ref('');
function addPlan() {
    const trimmedPlan = newPlan.value.trim();
    if (!trimmedPlan) {
        return;
    }

    emit('newCoffeePlan', trimmedPlan);
    newPlan.value = '';
} 
</script>

<template>    
    <form class="add-plan-form" @submit.prevent="addPlan">
      <input v-model.trim="newPlan" type="text" placeholder="Add a new plan" />
      <button class="btn btn-primary" type="submit" :disabled="newPlan.length < 5"
        @mouseenter="hover = true" @mouseleave="hover = false"
      >
        <slot name="btn" :hover="hover" />
      </button>
    </form>    
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