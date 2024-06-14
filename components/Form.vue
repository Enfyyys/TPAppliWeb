<template>
  <div>
    <div v-if="currentStep === 1">
      <Step1 :formData="formData" @nextStep="handleNextStep" />
    </div>
    <div v-else-if="currentStep === 2">
      <Step2 :formData="formData" @prevStep="prevStep" @nextStep="handleNextStep" />
    </div>
    <div v-else-if="currentStep === 3">
      <Step3 :formData="formData" @prevStep="prevStep" @nextStep="handleNextStep" />
    </div>
    <div v-else-if="currentStep === 4">
      <Step4 :formData="formData" @prevStep="prevStep" @submit="submitForm" />
    </div>
    <div v-else>
      <p>Étape inconnue</p>
    </div>
  </div>
</template>

<script>
import Step1 from '~/components/Step1.vue'
import Step2 from '~/components/Step2.vue'
import Step3 from '~/components/Step3.vue'
import Step4 from '~/components/Step4.vue'

export default {
  components: {
    Step1,
    Step2,
    Step3,
    Step4
  },
  data() {
    return {
      currentStep: 1,
      formData: {
        name: '',
        email: '',
        phone: '',
        message: ''
      }
    }
  },
  methods: {
    handleNextStep(data) {
      this.formData = { ...this.formData, ...data }
      this.nextStep()
    },
    nextStep() {
      this.currentStep++
    },
    prevStep() {
      this.currentStep--
    },
  }
}
</script>
