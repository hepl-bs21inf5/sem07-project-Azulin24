<script setup lang="ts">
import { ref, watch } from 'vue' // Import des fonctionnalités réactives et des observateurs de Vue.
import { QuestionState } from '@/utils/models' // Import de l'énumération `QuestionState` pour gérer les états des questions (vide, remplie, correcte, incorrecte, soumise, etc.).

const model = defineModel<QuestionState>() // Déclare un modèle réactif lié à l'état de la question. Permet une liaison bidirectionnelle entre le composant parent et ce composant enfant.
const props = defineProps<{
  id: string
  text: string
  answer: string | string[]
  answerDetail?: string
  placeholder?: string
}>() // Déclare les props attendues par le composant :
/*
  - `id` : Identifiant unique pour le champ de saisie (obligatoire).
  - `text` : Texte de la question (obligatoire).
  - `answer` : Réponse correcte, qui peut être une chaîne ou un tableau de chaînes (obligatoire).
  - `answerDetail` : Détails supplémentaires sur la réponse correcte (facultatif).
  - `placeholder` : Texte d'indication pour le champ de saisie (facultatif).
*/

const value = ref<string | null>(null) // Variable réactive qui contient la réponse saisie par l'utilisateur. Initialement `null`.

watch(model, (newModel) => {
  if (newModel === QuestionState.Submit) {
    // Vérifie si l'état de la question est "Submit".
    const possibleAnswers = Array.isArray(props.answer) ? props.answer : [props.answer] // Convertit `props.answer` en tableau si ce n'est pas déjà un tableau, pour gérer les réponses multiples.
    const isCorrect = possibleAnswers.some(
      (answer) => answer.toLowerCase() === (value.value || '').toLowerCase(),
    ) // Vérifie si la réponse de l'utilisateur (en ignorant la casse) correspond à l'une des réponses possibles.
    model.value = isCorrect ? QuestionState.Correct : QuestionState.Wrong // Met à jour l'état en fonction de la validité de la réponse (Correct ou Wrong).
  } else if (newModel === QuestionState.Empty) {
    // Réinitialise la réponse de l'utilisateur si l'état est "Empty".
    value.value = null
  }
})

watch(
  value,
  (newValue) => {
    if (newValue === null) {
      // Si aucune réponse n'est saisie, l'état est "Empty".
      model.value = QuestionState.Empty
    } else {
      // Si une réponse est saisie, l'état devient "Fill".
      model.value = QuestionState.Fill
    }
  },
  { immediate: true }, // Active immédiatement l'observateur avec la valeur initiale de `value`.
)
</script>

<template>
  <label :for="props.id" class="form-label"> {{ props.text }} </label>
  <!-- Affiche le texte de la question avec un label lié à l'identifiant du champ d'entrée. -->
  <input
    :id="props.id"
    v-model="value"
    class="form-control"
    :placeholder="props.placeholder"
    :disabled="
      model === QuestionState.Submit ||
      model === QuestionState.Correct ||
      model === QuestionState.Wrong
    "
  />
  <div v-if="model === QuestionState.Correct || model === QuestionState.Wrong">
    <!-- Affiche un message si l'état est "Correct" ou "Wrong". -->
    <p v-if="model === QuestionState.Correct" class="text-success">Juste !</p>
    <!-- Message "Juste !" en cas de réponse correcte. -->
    <p v-else class="text-danger">Faux ! La réponse était : {{ props.answer }}</p>
    <!-- Message "Faux !" avec la réponse correcte affichée. -->
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
    <!-- Affiche des détails supplémentaires sur la réponse correcte, s'ils sont fournis. -->
  </div>
</template>

<style scoped>
.text-danger {
  color: red !important; /* Style personnalisé pour les messages d'erreur, avec une priorité élevée grâce à `!important`. */
}
.text-success {
  color: blueviolet !important; /* Style personnalisé pour les messages de succès, avec une priorité élevée grâce à `!important`. */
}
</style>
