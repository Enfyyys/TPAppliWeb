<template>
    <div>
      <h1>Enregistrer ma position actuelle</h1>
      <v-text-field v-model="locationComment" label="Commentaire" placeholder="Ajouter un commentaire..."></v-text-field>
      <v-btn color="primary" @click="saveLocation">Enregistrer la position</v-btn>
  
      <div v-if="savedLocations.length > 0">
        <h2>Positions enregistrées</h2>
        <div v-for="(location, index) in savedLocations" :key="index">
          <p><strong>Commentaire:</strong> {{ location.comment }}</p>
          <p><strong>Latitude:</strong> {{ location.latitude }}</p>
          <p><strong>Longitude:</strong> {{ location.longitude }}</p>
          <v-btn color="error" @click="removeLocation(index)">Supprimer</v-btn>
        </div>
      </div>
      <div v-else>
        <p>Aucune position enregistrée.</p>
      </div>
  
      <v-snackbar v-model="snackbar" :timeout="snackbarTimeout" color="success">
        {{ snackbarMessage }}
        <v-btn text @click="snackbar = false">Fermer</v-btn>
      </v-snackbar>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        locationComment: '',
        savedLocations: [],
        snackbar: false,
        snackbarMessage: '',
        snackbarTimeout: 3000
      };
    },
    mounted() {
      this.getSavedLocations();
    },
    methods: {
      getSavedLocations() {
        try {
          this.savedLocations = JSON.parse(localStorage.getItem('savedLocations')) || [];
        } catch (error) {
          console.error('Erreur lors de la récupération des positions enregistrées:', error);
        }
      },
      saveLocation() {
        if (!navigator.geolocation) {
          this.showSnackbar('La géolocalisation n\'est pas supportée par votre navigateur.');
          return;
        }
  
        navigator.geolocation.getCurrentPosition(
          (position) => {
            const newLocation = {
              comment: this.locationComment,
              latitude: position.coords.latitude,
              longitude: position.coords.longitude
            };
            this.addLocation(newLocation);
            this.showSnackbar('Position enregistrée avec succès !');
          },
          (error) => {
            console.error('Erreur lors de la récupération de la position:', error);
            this.showSnackbar('Erreur lors de la récupération de la position.');
          }
        );
      },
      addLocation(location) {
        try {
          let savedLocations = JSON.parse(localStorage.getItem('savedLocations')) || [];
          savedLocations.push(location);
          localStorage.setItem('savedLocations', JSON.stringify(savedLocations));
          this.savedLocations = savedLocations;
          this.locationComment = '';  // Clear the comment input field
        } catch (error) {
          console.error('Erreur lors de l\'ajout de la position:', error);
        }
      },
      removeLocation(index) {
        try {
          let savedLocations = JSON.parse(localStorage.getItem('savedLocations')) || [];
          savedLocations.splice(index, 1);
          localStorage.setItem('savedLocations', JSON.stringify(savedLocations));
          this.savedLocations = savedLocations;
          this.showSnackbar('Position supprimée avec succès !');
        } catch (error) {
          console.error('Erreur lors de la suppression de la position:', error);
        }
      },
      showSnackbar(message) {
        this.snackbarMessage = message;
        this.snackbar = true;
      }
    }
  }
  </script>
  