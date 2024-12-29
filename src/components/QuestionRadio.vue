<script setup lang="ts">
import { computed, ref, watch, type PropType } from 'vue' // Importe les utilitaires de Vue.
import { QuestionState } from '@/utils/models' // Importe l'enum QuestionState.

const model = defineModel<QuestionState>() // État réactif pour la question.
const props = defineProps({
  // Propriétés pour configurer la question.
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  answerDetail: { type: String, default: '' },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})

const value = ref<string | null>(null) // Suivi de l'option sélectionnée.
const answerText = computed<string>( // Calcule le texte de la bonne réponse.
  () => props.options.find((option) => option.value === props.answer)?.text ?? props.answer,
)

watch(model, (newModel) => {
  // Valide la réponse lorsque l'état est "Submit".
  if (newModel === QuestionState.Submit) {
    model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value == null // Réinitialise la valeur si l'état est "Empty".
  }
})

watch(
  value,
  (newValue) => {
    // Met à jour l'état du modèle selon l'entrée.
    if (newValue === null) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true }, // Exécute cette logique immédiatement au montage du composant.
)
</script>

<template>
  {{ props.text }}
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="value"
      class="form-check-input"
      type="radio"
      :name="props.id"
      :value="option.value"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong
      "
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
  <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ answerText }}</p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>
<style scoped>
.text-danger {
  color: red !important;
}
.text-success {
  color: blueviolet !important;
}
</style>
