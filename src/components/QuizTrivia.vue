<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue' // Import du composant QuestionRadio qui est utilisé pour afficher des questions à choix multiples.
import { reactive, ref, computed } from 'vue' // Import des fonctions réactives de Vue pour créer des variables réactives et des propriétés calculées.
import { QuestionState } from '@/utils/models' // Import de l'enum QuestionState pour gérer les différents états de la question.

const questions = ref<
  {
    question: string
    correct_answer: string
    incorrect_answers: string[]
  }[]
>([]) //référence réactive qui contiendra un tableau de questions obtenues via une API. Chaque question est un objet avec une question, une réponse correcte et des réponses incorrectes.

const questionStates = ref<QuestionState[]>([]) // référence réactive contenant un tableau d'états correspondant à chaque question (réponse vide, remplie, correcte, incorrecte, etc.).

const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Fill),
) // propriété calculée qui indique si toutes les questions ont été remplies par l'utilisateur (toutes les réponses ne sont pas vides).

const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
) // propriété calculée qui compte le nombre de réponses correctes en fonction des états des questions.

const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
) // propriété calculée qui indique si toutes les questions ont été soumises (réponses correctes ou incorrectes).

const totalScore = computed<number>(() => questionStates.value.length) // propriété calculée qui donne le nombre total de questions.

const answers = reactive<{ [key: number]: QuestionState }>({}) // associe à chaque question son état

function reset(event: Event): void {
  event.preventDefault() // Empêche le comportement par défaut de l'événement (rechargement de la page).
  questionStates.value = questionStates.value.map(() => QuestionState.Empty) // Réinitialise l'état de toutes les questions à "Empty".
}

function submit(event: Event): void {
  event.preventDefault() // Empêche le comportement par défaut de l'événement.
  questionStates.value = questionStates.value.map(() => QuestionState.Submit) // Soumet les réponses, en mettant l'état de chaque question à "Submit".
}

// Appel de l'API Open Trivia pour récupérer des questions au format JSON.
fetch('https://opentdb.com/api.php?amount=10&type=multiple')
  .then((response) => response.json())
  .then((data) => {
    questions.value = data.results // met les questions dans la variable "questions"
    questions.value.forEach((_, index) => {
      answers[index] = QuestionState.Empty // au début l'état de chaque question est empty
      questionStates.value.push(QuestionState.Empty) // ajoute les états à "questionStates"
    })
  })
</script>

<template>
  <form @submit="submit">
    <!-- Le formulaire pour la soumission des réponses. -->
    <QuestionRadio
      v-for="(question, index) in questions"
      :id="index.toString()"
      :key="index"
      v-model="questionStates[index]"
      :text="question.question"
      :options="[
        { value: question.correct_answer, text: question.correct_answer },
        ...question.incorrect_answers.map((answer) => ({
          value: answer,
          text: answer,
        })),
      ]"
    />
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <!-- Bouton pour soumettre le formulaire, désactivé tant que toutes les questions ne sont pas remplies. -->
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
    <!-- Bouton pour réinitialiser les réponses. -->
    <div v-if="submitted">Score: {{ score }} / {{ totalScore }}</div>
    <!-- Affichage du score total si toutes les questions ont été soumises. -->
  </form>
</template>
