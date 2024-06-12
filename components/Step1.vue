<!-- Step1.vue -->
<template>
    <div>
      <v-form @submit.prevent="validateStep">
        <v-text-field v-model="formData.name" label="Nom"></v-text-field>
        <v-text-field v-model="formData.email" label="Email"></v-text-field>
        <v-btn type="submit">Suivant</v-btn>
      </v-form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          name: '',
          email: ''
        }
      }
    },
    methods: {
      validateStep() {
        // Validation des champs, par exemple
        if (!this.formData.name || !this.formData.email) {
          alert('Veuillez remplir tous les champs')
          return
        }
        this.$emit('nextStep', this.formData)
      }
    }
  }
  </script>
  