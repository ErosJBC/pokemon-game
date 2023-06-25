<template>
    <div class="h-[200px] flex justify-center relative">
        <img :src="imgSrc" class="absolute h-[200px] user-select hidden-pokemon" alt="pokemon">
        <img v-if="showPokemon" :src="imgSrc" class="fade-in absolute h-[200px] user-select" alt="pokemon">
    </div>
</template>

<script>
export default {
    name: "PokemonPicture",
    props: {
        pokemonId: {
            type: Number,
            required: true,
        },
        showPokemon: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
        }
    }
}
</script>

<style scoped>

.user-select {
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-select: none;
    -webkit-user-drag: none;
}
.hidden-pokemon {
    filter: brightness(0);
}
</style>