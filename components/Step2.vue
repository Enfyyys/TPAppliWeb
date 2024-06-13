<template>
    <div>
      <v-form @submit.prevent="validateStep">
        <v-text-field v-model="formData.phone" label="Téléphone" type="number" counter="10"></v-text-field>
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
        if (!this.formData.phone) {
          alert('Veuillez remplir tous les champs')
          return
        }
        this.$emit('nextStep', this.formData)
      }
    }
  }
  </script>
  