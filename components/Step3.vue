<!-- Step3.vue -->
<template>
    <div>
      <v-form @submit.prevent="submitForm">
        <v-textarea v-model="formData.message" label="Message"></v-textarea>
        <v-btn @click="$emit('prevStep')">Précédent</v-btn>
        <v-btn type="submit">Soumettre</v-btn>
        <v-dialog v-model="dialog" max-width="600">
          <v-card>
            <v-card-title class="headline">Validation</v-card-title>
            <v-card-text>
              Merci pour votre message! Nous vous répondrons dès que possible.
            </v-card-text>
            <v-card-actions>
              <v-btn color="primary" @click="dialog = false">OK</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          message: ''
        },
        dialog: false
      }
    },
    methods: {
      submitForm() {
        // Validation des champs, par exemple
        if (!this.formData.message) {
          alert('Veuillez remplir tous les champs')
          return
        }
        // Afficher le faux texte de validation
        this.dialog = true;
      }
    }
  }
  </script>
  