<template>
    <v-card class="card-with-hover">
        <figure>
            <v-img :src="props.photo" alt="Photo de chat" width="450" height="350" class="catimg"></v-img>
            <figcaption>Poti chat</figcaption>
        </figure>
    </v-card>
</template>

<script setup>
    const props = defineProps(['photo'])
</script>

<style scoped>
.card-with-hover {
    overflow: visible; /* Permet à l'image de dépasser les limites de la carte */
    position: relative; /* Assure que la carte est le contexte d'empilement pour les éléments fils positionnés */
}

.card-with-hover .catimg {
    transition: transform 0.3s ease; /* Animation de transition pour une expérience visuelle fluide */
}

.card-with-hover:hover .catimg {
    transform: scale(1.2); /* Agrandit l'image de 20% au survol */
    position: relative; /* Nécessaire pour s'assurer que l'image peut dépasser les limites de la carte */
    z-index: 1; /* Assure que l'image agrandie est au-dessus du contenu de la carte */
}
</style>
