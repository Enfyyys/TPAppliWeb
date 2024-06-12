<!-- Step2.vue -->
<template>
    <div>
      <v-form @submit.prevent="validateStep">
        <v-text-field v-model="formData.phone" label="Téléphone"></v-text-field>
        <v-btn @click="$emit('prevStep')">Précédent</v-btn>
        <v-btn type="submit">Suivant</v-btn>
      </v-form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          phone: ''
        }
      }
    },
    methods: {
      validateStep() {
        // Validation des champs, par exemple
        if (!this.formData.phone) {
          alert('Veuillez remplir tous les champs')
          return
        }
        this.$emit('nextStep', this.formData)
      }
    }
  }
  </script>
  