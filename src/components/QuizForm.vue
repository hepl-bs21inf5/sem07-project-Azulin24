<script setup lang="ts">
import { computed, ref, watch } from 'vue';
import QuestionRadio from '@/components/QuestionRadio.vue';
import QuestionText from '@/components/QuestionText.vue';
import QuestionCheckbox from '@/components/QuestionCheckbox.vue';

const correctAnswersData = {
  MachuPicchu: 'Inca',
  Gastronomie: 'Lima',
  oiseau: 'Condor',
  attractions_Perou: ['Machu_Picchu', 'Nazca', 'Sacsayhuaman']
};

const correctAnswers = ref<boolean[]>([false, false, false, false]);

const MachuPicchu = ref<string | null>(null);
const Gastronomie = ref<string | null>(null);
const oiseau = ref<string | null>(null);
const attractions_Perou = ref<string[]>([]);

const filled = computed<boolean>(() => correctAnswers.value.length === 4);
const score = computed<number>(() => correctAnswers.value.filter((value) => value).length);

const totalScore = computed<number>(() => Object.keys(correctAnswersData).length);

const updateCorrectAnswers = () => {
  correctAnswers.value = [
    MachuPicchu.value === correctAnswersData.MachuPicchu,
    Gastronomie.value === correctAnswersData.Gastronomie,
    oiseau.value === correctAnswersData.oiseau,
    JSON.stringify(attractions_Perou.value.sort()) === JSON.stringify(correctAnswersData.attractions_Perou.sort())
  ];
};

watch([MachuPicchu, Gastronomie, oiseau, attractions_Perou], updateCorrectAnswers, { deep: true, immediate: true });

function submit(event: Event): void {
  event.preventDefault();
}
function reset(): void {
  MachuPicchu.value = null;
  Gastronomie.value = null;
  oiseau.value = null;
  attractions_Perou.value = [];
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      id="MachuPicchu"
      v-model="MachuPicchu"
      answer="MachuPicchu"
      text="Quelle ancienne civilisation a construit le Machu Picchu ?"
      :options="[
        { value: 'Maya', text: 'Les Mayas' },
        { value: 'Aztheque', text: 'Les Aztèques' },
        { value: 'Inca', text: 'Les Incas' },
        { value: 'Olmeque', text: 'Les Olmèques' }
      ]"
    />
    <div>Réponse correcte : {{ correctAnswers[0] }}</div>

    <QuestionText
      id="Gastronomie"
      v-model="Gastronomie"
      answer="Lima"
      text="Quelle est la capitale gastronomique de l'Amérique latine ?"
      placeholder="Veuillez saisir un mot"
    />
    <div>Réponse correcte : {{ correctAnswers[1] }}</div>

    <QuestionRadio
      id="oiseau"
      v-model="oiseau"
      answer="Condor"
      text="Quel est le nom de l'oiseau national du Pérou ?"
      :options="[
        { value: 'Condor', text: 'Le condor des Andes' },
        { value: 'Toucan', text: 'Le toucan' },
        { value: 'Coq', text: 'Le coq-de-roche péruvien' },
        { value: 'Aigle', text: `L'aigle royal` }
      ]"
    />
    <div>Réponse correcte : {{ correctAnswers[2] }}</div>

    <QuestionCheckbox
      id="attractions_Perou"
      v-model="attractions_Perou"
      text="Quelles sont les attractions célèbres du Pérou ? (sélectionnez toutes les réponses pertinentes)"
      :options="[
        { value: 'Machu_Picchu', text: 'Machu Picchu' },
        { value: 'Nazca', text: 'Les lignes de Nazca' },
        { value: 'Sacsayhuaman', text: 'Sacsayhuamán' },
        { value: 'Titicaca', text: 'Le lac Titicaca' },
        { value: 'Amazonie', text: 'La forêt amazonienne' }
      ]"
    />
    <div>Réponse correcte : {{ correctAnswers[3] }}</div>

    <div>Score : {{ score }} / {{ totalScore }}</div>

    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button class="btn btn-secondary" @click="reset" type="button">Réinitialiser</button>
  </form>
</template>
