<template>
  <div>
    <v-form @submit.prevent="validateStep">
      <v-text-field v-model="localFormData.name" label="Nom"></v-text-field>
      <v-text-field v-model="localFormData.email" label="Email"></v-text-field>
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
    validateStep() {
      if (!this.localFormData.name || !this.localFormData.email) {
        alert('Veuillez remplir tous les champs')
        return
      }
      this.$emit('nextStep', this.localFormData)
    }
  }
}
</script>
