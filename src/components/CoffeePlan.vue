<script setup lang="ts">
import { defineProps } from 'vue'

defineProps({
  name: {
    type: String,
    default: 'Default Plan',
  },
})
</script>

<template>
  <div class="plan">
    <div class="description">
      <span class="title"> {{ name }} </span>
    </div>
  </div>
</template>

<style scoped></style>
