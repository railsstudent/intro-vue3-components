<script setup lang="ts">
import { defineProps } from 'vue'

const props = defineProps({
  name: {
    type: String,
    default: 'Default Plan',
  },
})
</script>

<template>
  <div class="plan">
    <div class="description">
      <span class="title"> {{ props.name }} </span>
    </div>
  </div>
</template>

<style scoped></style>
