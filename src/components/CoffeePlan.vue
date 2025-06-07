<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps({
  name: {
    type: String,
    default: 'Default Plan',
  },
  selected: {
    type: Boolean,
    default: false,
  },
})

const emit = defineEmits<{
  (e: 'selectedPlan', name: string): void
}>()

function selectPlan() {
  emit('selectedPlan', props.name)
}

const iconsNames = computed(() => {
		return props.name.startsWith('The')  ? ['ic:outline-coffee', 'ic:outline-coffee-maker'] : [
			'ic:outline-emoji-food-beverage', 'ic:outline-fastfood'
		];
	});
</script>

<template>
  <div class="plan" @click="selectPlan" :class="{ 'active-plan': selected }">
    <template v-if="$slots.icon">
      <slot name="icon" :iconsNames="iconsNames"  />
    </template>
    <div class="description">
      <span class="title"> {{ name }} </span>
    </div>
  </div>
</template>

<style scoped></style>
