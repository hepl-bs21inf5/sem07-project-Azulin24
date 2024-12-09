<script setup lang="ts">
import { ref, defineProps, defineEmits, watch, type PropType } from 'vue'

const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  modelValue: { type: String, default: '' },
  placeholder: String,
})

const emit = defineEmits(['update:modelValue'])
const localValue = ref(props.modelValue)

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
      placeholder="Veuillez saisir un mot"
      @input="updateValue"
    />
  </div>
</template>
