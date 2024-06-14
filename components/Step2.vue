<template>
  <div>
    <v-form @submit.prevent="validateStep">
      <v-text-field v-model="localFormData.phone" label="Téléphone" type="number" counter="10"></v-text-field>
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
    validateStep() {
      if (!this.localFormData.phone) {
        alert('Veuillez remplir tous les champs')
        return
      }
      this.$emit('nextStep', this.localFormData)
    }
  }
}
</script>
