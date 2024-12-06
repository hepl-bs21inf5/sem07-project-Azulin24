<script setup lang="ts">
import { defineProps, ref, watch } from 'vue'

// Définir les propriétés que le composant recevra
const { id, text, options, modelValue } = defineProps<{
  id: string
  text: string
  options: { value: string; text: string }[]
  modelValue: string[]
}>()

// Utilisation d'une variable locale pour suivre les réponses sélectionnées
const selectedAnswers = ref<string[]>(modelValue)

// Émettre la mise à jour vers le parent lorsqu'une option est sélectionnée/désélectionnée
watch(selectedAnswers, (newValue) => {
  emit('update:modelValue', newValue)
})
</script>

<template>
  <div :id="id">
    <p>{{ text }}</p>
    <div v-for="(option, index) in options" :key="index" class="form-check">
      <input
        type="checkbox"
        :value="option.value"
        :id="option.value"
        v-model="selectedAnswers"
        class="form-check-input"
      />
      <label class="form-check-label" :for="option.value">{{ option.text }}</label>
    </div>
  </div>
</template>
