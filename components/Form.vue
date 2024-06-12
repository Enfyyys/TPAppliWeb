<template>
    <div>
      <!-- Étape 1 -->
      <div v-if="currentStep === 1">
        <Step1 @nextStep="nextStep" />
      </div>
      <!-- Étape 2 -->
      <div v-else-if="currentStep === 2">
        <Step2 @prevStep="prevStep" @nextStep="nextStep" />
      </div>
      <!-- Étape 3 -->
      <div v-else-if="currentStep === 3">
        <Step3 @prevStep="prevStep" @submit="submitForm" />
      </div>
      <!-- Autre -->
      <div v-else>
        <p>Étape inconnue</p>
      </div>
    </div>
  </template>
  
  <script>
  import Step1 from '~/components/Step1.vue'
  import Step2 from '~/components/Step2.vue'
  import Step3 from '~/components/Step3.vue'
  
  export default {
    components: {
      Step1,
      Step2,
      Step3
    },
    data() {
      return {
        currentStep: 1
      }
    },
    methods: {
      nextStep() {
        this.currentStep++
      },
      prevStep() {
        this.currentStep--
      },
      submitForm(formData) {
        // Envoyer le formulaire avec les données
      }
    }
  }
  </script>
  