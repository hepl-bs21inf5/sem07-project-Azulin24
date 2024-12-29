<script setup lang="ts">
import { defineProps, defineModel, ref, watch, type PropType } from 'vue'
import { QuestionState } from '@/utils/models'

// Définition du modèle `model` pour gérer l'état de la question
const model = defineModel<QuestionState>()

// Définition des props du composant
const props = defineProps({
  id: { type: String, required: true }, // Identifiant unique de la question
  text: { type: String, required: true }, // Texte de la question
  answer: { type: Array as PropType<string[]>, required: true }, // Liste des réponses correctes
  answerDetail: { type: String, default: '' }, // Détail ou explication en cas de réponse incorrecte (optionnel)
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>, // Liste des options proposées pour la question
    required: true,
  },
})

// Définition de la variable réactive `value` qui contiendra les réponses de l'utilisateur
const value = ref<string[]>([])

// Premier `watch` qui surveille la variable `value` (réponses de l'utilisateur)
watch(
  value,
  (newValue) => {
    if (newValue.length === 0) {
      model.value = QuestionState.Empty // Si aucune réponse n'est sélectionnée, l'état de la question est "Empty"
    } else {
      model.value = QuestionState.Fill // Si des réponses sont sélectionnées, l'état est "Fill"
    }
  },
  { immediate: true }, // On exécute ce `watch` immédiatement au démarrage
)

// Deuxième `watch` qui surveille le modèle `model` (l'état de la question)
watch(model, (newModel) => {
  if (newModel === QuestionState.Submit) {
    // Si la question est soumise, on vérifie si les réponses sont correctes
    const isCorrect =
      props.answer.length === value.value.length && // Vérifie que le nombre de réponses est le même
      props.answer.every((val) => value.value.includes(val)) // Vérifie que chaque réponse correcte est sélectionnée
    model.value = isCorrect ? QuestionState.Correct : QuestionState.Wrong // Marque la question comme "Correct" ou "Wrong"
  } else if (newModel === QuestionState.Empty) {
    value.value = [] // Si l'état de la question est "Empty", on réinitialise les réponses de l'utilisateur
  }
})
</script>

<template>
  <p>{{ text }}</p>
  <!-- Affichage du texte de la question -->

  <!-- Boucle pour afficher chaque option de la question -->
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="value"
      class="form-check-input"
      type="checkbox"
      :value="option.value"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong
      "
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">{{ option.text }}</label>
    <!-- Affichage du texte de l'option -->
  </div>
  <!-- Section d'affichage du feedback après soumission -->
  <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <!-- Message de succès si la réponse est correcte -->
    <p v-else class="text-danger">
      Faux ! Les réponses étaient : {{ answer[0] }}, {{ answer[1] }} et {{ answer[2] }}
      <!-- Message d'erreur avec les réponses correctes -->
    </p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
    <!-- Affichage des détails de l'explication des réponses -->
  </div>
</template>
<style scoped>
.text-danger {
  color: red !important; /* Texte rouge pour les réponses incorrectes */
}
.text-success {
  color: blueviolet !important; /* Texte violet pour les réponses correctes */
}
</style>
