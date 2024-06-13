<template>
  <div>
    <h1>Mes Photos de Chat</h1>
    <v-btn color="primary" @click="fetchAndStoreCatPhoto">Ajouter une photo de chat</v-btn>
    <div v-if="catPhotos.length > 0">
      <v-row justify="space-around">
        <v-col v-for="(photo, index) in catPhotos" :key="index" cols="12" sm="6" md="4">
          <cat :photo="photo"></cat>
          <v-btn color="error" @click="removeCatPhoto(index)">Supprimer</v-btn>
          <v-btn color="primary" @click="shareCatPhoto(photo)">Partager</v-btn>
        </v-col>
      </v-row>
    </div>
    <div v-else>
      <p>Aucune photo de chat sauvegardée.</p>
    </div>
    

    <v-snackbar v-model="snackbar" :timeout="snackbarTimeout" color="success">
      {{ snackbarMessage }}
      <v-btn text @click="snackbar = false">Fermer</v-btn>
    </v-snackbar>
  </div>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      catPhotos: [],
      snackbar: false,
      snackbarMessage: '',
      snackbarTimeout: 3000
    };
  },
  mounted() {
    this.getCatPhotos();
  },
  methods: {
    async getCatPhotos() {
      try {
        this.catPhotos = JSON.parse(localStorage.getItem('catPhotos')) || [];
      } catch (error) {
        console.error('Erreur lors de la récupération des photos de chat:', error);
      }
    },
    async fetchAndStoreCatPhoto() {
      try {
        const response = await axios.get('https://api.thecatapi.com/v1/images/search?limit=1');
        const photoUrl = response.data[0].url;
        this.addCatPhoto(photoUrl);
        this.showSnackbar('Photo de chat ajoutée avec succès !');
      } catch (error) {
        console.error('Erreur lors de la récupération de la photo de chat:', error);
      }
    },
    async addCatPhoto(photoUrl) {
      try {
        let catPhotos = JSON.parse(localStorage.getItem('catPhotos')) || [];
        catPhotos.push(photoUrl);
        localStorage.setItem('catPhotos', JSON.stringify(catPhotos));
        this.catPhotos = catPhotos;
      } catch (error) {
        console.error('Erreur lors de l\'ajout de la photo de chat:', error);
      }
    },
    removeCatPhoto(index) {
      try {
        let catPhotos = JSON.parse(localStorage.getItem('catPhotos')) || [];
        catPhotos.splice(index, 1);
        localStorage.setItem('catPhotos', JSON.stringify(catPhotos));
        this.catPhotos = catPhotos;
        this.showSnackbar('Photo de chat supprimée avec succès !');
      } catch (error) {
        console.error('Erreur lors de la suppression de la photo de chat:', error);
      }
    },
    showSnackbar(message) {
      this.snackbarMessage = message;
      this.snackbar = true;
    },
    shareCatPhoto(photoUrl) {
      if (navigator.share) {
        navigator.share({
          title: 'Photo de chat',
          text: 'Regardez cette adorable photo de chat !',
          url: photoUrl
        }).then(() => {
          this.showSnackbar('Photo de chat partagée avec succès !');
        }).catch((error) => {
          console.error('Erreur lors du partage de la photo de chat:', error);
          this.showSnackbar('Erreur lors du partage de la photo de chat.');
        });
      } else {
        this.showSnackbar('Partage non supporté sur cet appareil.');
      }
    }
  }
}
</script>

