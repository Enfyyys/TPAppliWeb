<template>
  <v-app-bar app>
    <v-toolbar-title>Mon Application</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn text :to="{ name: 'index' }">Accueil</v-btn>
    <v-btn text :to="{ name: 'cat' }">Photos de chats</v-btn>
    <v-btn text :to="{ name: 'geolocation' }">Géolocalisation</v-btn>
    <v-btn text :to="{ name: 'about' }">À propos</v-btn>
    <v-btn text :to="{ name: 'contact' }">Contact</v-btn>
  </v-app-bar>
</template>

<script setup>
import { VAppBar, VToolbarTitle, VSpacer, VBtn } from 'vuetify/components'
</script>

<style scoped>
/* Ajoutez ici vos styles personnalisés si nécessaire */
</style>
