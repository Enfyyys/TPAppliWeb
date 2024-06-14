<template>
    <div>
      <v-card>
        <v-card-title>Validation des informations</v-card-title>
        <v-card-text>
          <p><strong>Nom:</strong> {{ formData.name }}</p>
          <p><strong>Email:</strong> {{ formData.email }}</p>
          <p><strong>Téléphone:</strong> {{ formData.phone }}</p>
          <p><strong>Message:</strong> {{ formData.message }}</p>
        </v-card-text>
        <v-card-actions>
          <v-btn @click="$emit('prevStep')">Précédent</v-btn>
          <v-btn @click="validateAndSubmit">Soumettre</v-btn>
        </v-card-actions>
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
      </v-card>
    </div>
  </template>
  
  <script>
  export default {
    props: ['formData'],
    data() {
      return {
        dialog: false
      }
    },
    methods: {
      validateAndSubmit() {
        if (!this.formData.message) {
          alert('Veuillez remplir tous les champs')
          return
        }
        this.dialog = true
        this.$emit('submit', this.formData)
      }
    }
  }
  </script>
  