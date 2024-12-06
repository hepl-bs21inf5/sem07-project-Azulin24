<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'

const MachuPicchu = ref<string | null>(null);
const Gastronomie = ref<string | null>(null);
const oiseau = ref<string | null>(null);
const attractions_Perou = ref<string[]>([]);
const filled = computed<boolean>(
  () => oiseau.value !== null && MachuPicchu.value !== null && Gastronomie.value !== null,
);
const correctAnswers = ['Machu_Picchu', 'Nazca', 'Sacsayhuaman'];
const userAnswers = attractions_Perou.value ;

function submit(event: Event): void {
  event.preventDefault()
  let score = 0
  if (MachuPicchu.value == 'Inca') score++
  if (oiseau.value == 'Condor') score++
  if (Gastronomie.value == 'Lima') score++
  if (userAnswers  == correctAnswers ) score++

  switch (score) {
    case 4:
      alert(
        `C'est tout juste : ${MachuPicchu.value}, ${Gastronomie.value}, ${oiseau.value} et les attractions. 4/4 Bravo !`,
      )
      break
    case 3:
      alert(`Presque parfait, vous avez 3 réponses correctes.`)
      break
    case 2:
      alert(`Presque parfait, vous avez 2 réponses correctes.`)
      break
    case 1:
      alert(`Vous avez 1 réponse juste.`)
      break
    case 0:
      alert(`Vous avez 0 réponse juste.`)
      break
  }
}
function reset(): void {
  MachuPicchu.value = null
  Gastronomie.value = null
  oiseau.value = null
  attractions_Perou.value = []
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      id="MachuPicchu"
      v-model="MachuPicchu"
      text="Quelle ancienne civilisation a construit le Machu Picchu ?"
      :options="[
        { value: 'Maya', text: 'Les Mayas' },
        { value: 'Aztheque', text: 'Les Aztèques' },
        { value: 'Inca', text: 'Les Incas' },
        { value: 'Olmeque', text: 'Les Olmèques' },
      ]"
    />
    <QuestionText
      id="Gastronomie"
      v-model="Gastronomie"
      text="Quelle est la capitale gastronomique de l'Amérique latine ?"
      placeholder="Veuillez saisir un nombre"
    />
    <QuestionRadio
      id="oiseau"
      v-model="oiseau"
      text="Quel est le nom de l'oiseau national du Pérou ?"
      :options="[
        { value: 'Condor', text: 'Le condor des Andes' },
        { value: 'Toucan', text: 'Le toucan' },
        { value: 'Coq', text: 'Le coq-de-roche péruvien' },
        { value: 'Aigle', text: `L'aigle royal` },
      ]"
    />
    <QuestionCheckbox
      id="attractions_Perou"
      v-model="attractions_Perou"
      text="Quelles sont les attractions célèbres du Pérou ? (sélectionnez toutes les réponses pertinentes)"
      :options="[
        { value: 'Machu_Picchu', text: 'Machu Picchu' },
        { value: 'Nazca', text: 'Les lignes de Nazca' },
        { value: 'Sacsayhuaman', text: 'Sacsayhuamán' },
        { value: 'Titicaca', text: 'Le lac Titicaca' },
        { value: 'Amazonie', text: 'La forêt amazonienne' },
      ]"
    />
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button class="btn btn-secondary" @click="reset" type="button">Réinitialiser</button>
  </form>
</template>
