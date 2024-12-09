<script setup lang="ts">
import { defineProps, defineEmits, ref, watch } from 'vue';

// Définir les propriétés que le composant recevra
const props = defineProps<{
  id: string;
  text: string;
  options: { value: string; text: string }[];
  modelValue: string[];
}>();

// Émettre l'événement pour la mise à jour de la valeur
const emit = defineEmits(['update:modelValue']);

// Utilisation d'une variable locale pour suivre les réponses sélectionnées
const selectedAnswers = ref<string[]>(props.modelValue);

// Regarder les changements sur la prop `modelValue` pour synchroniser la valeur
watch(() => props.modelValue, (newValue) => {
  selectedAnswers.value = newValue;
});

// Émettre la mise à jour vers le parent lorsqu'une option est sélectionnée/désélectionnée
watch(selectedAnswers, (newValue) => {
  emit('update:modelValue', newValue);
});
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

