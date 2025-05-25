<script setup lang="ts">
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
</script>

<template>
  <div class="plan" @click="selectPlan" :class="{ 'active-plan': selected }">
    <div class="description">
      <span class="title"> {{ name }} </span>
    </div>
  </div>
</template>

<style scoped></style>
