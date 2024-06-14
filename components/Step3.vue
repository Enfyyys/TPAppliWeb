<template>
  <div>
    <v-form @submit.prevent="nextStep">
      <v-textarea v-model="localFormData.message" label="Message"></v-textarea>
      <v-btn @click="$emit('prevStep')">Précédent</v-btn>
      <v-btn type="submit">Suivant</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  props: ['formData'],
  data() {
    return {
      localFormData: { ...this.formData }
    }
  },
  methods: {
    nextStep() {
      this.$emit('nextStep', this.localFormData)
    }
  }
}
</script>
