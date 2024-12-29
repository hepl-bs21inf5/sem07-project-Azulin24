<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'
import { QuestionState } from '@/utils/models'

// Définition de la liste des états de chaque question
const questionStates = ref<QuestionState[]>([])

// Calcul si toutes les questions ont été remplies (toutes les questions sont à l'état "Fill")
const filled = computed<boolean>(
  () => questionStates.value.every((state) => state === QuestionState.Fill), // Vérifie si toutes les réponses sont remplies
)

// Calcul de l'état "submit" : vérifie si toutes les questions ont été soumises (c'est-à-dire toutes les questions sont "Correct" ou "Wrong")
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

// Calcul du score en comptant les bonnes réponses ("Correct")
const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)

// Le score total est simplement le nombre de questions
const totalScore = computed<number>(() => questionStates.value.length)

// Fonction de réinitialisation des états des questions à "Empty" (aucune réponse)
function reset(event: Event): void {
  event.preventDefault() // Empêche le comportement par défaut du formulaire
  questionStates.value = questionStates.value.map(() => QuestionState.Empty) // Réinitialise toutes les réponses
}

// Fonction pour soumettre les réponses, change l'état des questions à "Submit"
function submit(event: Event): void {
  event.preventDefault() // Empêche le comportement par défaut du formulaire
  questionStates.value = questionStates.value.map(() => QuestionState.Submit) // Marque toutes les questions comme soumises
}
</script>

<template>
  <form @submit="submit">
    <!-- Question 1: QuestionRadio -->
    <QuestionRadio
      answer-detail="Les Incas ont construit Machu Picchu"
      id="MachuPicchu"
      v-model="questionStates[0]"
      answer="Inca"
      text="Quelle ancienne civilisation a construit le Machu Picchu ?"
      :options="[
        { value: 'Maya', text: 'Les Mayas' },
        { value: 'Aztheque', text: 'Les Aztèques' },
        { value: 'Inca', text: 'Les Incas' },
        { value: 'Olmeque', text: 'Les Olmèques' },
      ]"
    />

    <!-- Question 2: QuestionText -->
    <QuestionText
      answer-detail="Lima est la capitale gastronomique de l'Amérique Latine"
      id="Gastronomie"
      v-model="questionStates[1]"
      :answer="['lima']"
      text="Quelle est la capitale gastronomique de l'Amérique latine ?"
      placeholder="Veuillez saisir un mot"
    />
    <!-- Question 3: QuestionRadio -->
    <QuestionRadio
      answer-detail="Le condor des Andes est l'oiseau national du Pérou"
      id="oiseau"
      v-model="questionStates[2]"
      answer="Condor"
      text="Quel est le nom de l'oiseau national du Pérou ?"
      :options="[
        { value: 'Condor', text: 'Le condor des Andes' },
        { value: 'Toucan', text: 'Le toucan' },
        { value: 'Coq', text: 'Le coq-de-roche péruvien' },
        { value: 'Aigle', text: `L'aigle royal` },
      ]"
    />
    <!-- Question 4: QuestionCheckbox -->
    <QuestionCheckbox
      id="attractions_Perou"
      v-model="questionStates[3]"
      text="Quelles sont les attractions célèbres du Pérou ? (sélectionnez toutes les réponses pertinentes)"
      :answer="['Machu_Picchu', 'Nazca', 'Sacsayhuaman']"
      answer-detail="Machu Picchu, Nazca et Sacsayhuaman sont les attractions célèbres du Pérou "
      :options="[
        { value: 'Machu_Picchu', text: 'Machu Picchu' },
        { value: 'Nazca', text: 'Les lignes de Nazca' },
        { value: 'Sacsayhuaman', text: 'Sacsayhuamán' },
        { value: 'Titicaca', text: 'Le lac Titicaca' },
        { value: 'Amazonie', text: 'La forêt amazonienne' },
      ]"
    />
    <br />
    <!-- Boutons de soumission et réinitialisation -->
    <button class="btn btn-primary" :class="{ disabled: !filled }" @click="submit">Terminer</button>
    &nbsp;
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>

    <!-- Debug affichant l'état actuel des réponses -->
    <div>Debug états : {{ questionStates }}</div>

    <!-- Affichage du score une fois les réponses soumises -->
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
  </form>
</template>
