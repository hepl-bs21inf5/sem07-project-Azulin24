<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps({
  id: String,
  text: String,
  placeholder: String,
  modelValue: String,
})
const emit = defineEmits(['update:modelValue'])

const localValue = ref(props.modelValue || '')

watch(
  () => props.modelValue,
  (newValue) => {
    localValue.value = newValue
  },
)

function updateValue() {
  emit('update:modelValue', localValue.value)
}
</script>

<template>
  <div>
    <label for="id" class="form-label"> {{ text }} </label>
    <input
      :id="id"
      v-model="localValue"
      class="form-control"
      placeholder="Veuillez saisir un nombre"
      @input="updateValue"
    />
  </div>
</template>
