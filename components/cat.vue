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
    overflow: visible;
    position: relative;
}

.card-with-hover .catimg {
    transition: transform 0.3s ease;
}

.card-with-hover:hover .catimg {
    transform: scale(1.2);
    position: relative;
    z-index: 1;
}
</style>
