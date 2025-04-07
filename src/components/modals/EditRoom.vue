<template>
  <v-dialog v-model="dialogModel" @update:modelValue="close" max-width="500">
    <v-card>
      <v-card-title>Editar sala</v-card-title>

      <v-card-text>
        <v-text-field label="Sala" v-model="room.room" />
        <v-text-field label="Professor" v-model="room.teacher" />
        <v-text-field label="Status" v-model="room.status" />
      </v-card-text>

      <v-card-actions>
        <v-spacer />
        <v-btn text @click="close">Cancelar</v-btn>
        <v-btn color="primary" @click="save">Salvar</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script setup lang="ts">
const props = defineProps({
  modelValue: Boolean,
  room: Object,
})

const room = ref({...props.room})
const emit = defineEmits(['update:modelValue', 'save'])

watch(
  () => props.room,
  (newVal) => {
    room.value = { ...newVal }
  },
  { immediate: true }
)

const dialogModel = computed({
  get: () => props.modelValue,
  set: (val) => emit('update:modelValue', val),
})

function close() {
  emit('update:modelValue', false)
}

function save() {
  emit('save', room.value)
  emit('update:modelValue', false)
}
</script>
