<template>
    <h1 class="text-3xl font-bold" v-if="!pokemon">Espere por favor...</h1>
    <div v-else>
        <h1 class="text-3xl font-bold pb-6">¿Quién es este pokemón?</h1>
        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
        <PokemonOptions
            :pokemons="pokemonArr"
            @selection="checkAnswer"
            :disabled="showAnswer"
        />

        <template v-if="showAnswer">
            <h2 class="fade-in mt-6 text-xl font-medium">{{ message }}</h2>
            <button
                @click="newGame"
                class="mt-6 text-white bg-slate-800 py-1 text-[15px] px-6 rounded flex gap-x-1 items-center justify-center mx-auto"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="16"
                    height="16"
                    fill="currentColor"
                    class="bi bi-arrow-clockwise"
                    viewBox="0 0 16 16"
                >
                    <path
                        fill-rule="evenodd"
                        d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z"
                    />
                    <path
                        d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z"
                    />
                </svg>
                Reiniciar
            </button>
        </template>
    </div>
</template>

<script>
import PokemonOptions from "@/components/PokemonOptions.vue";
import PokemonPicture from "@/components/PokemonPicture.vue";
import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
    name: "PokemonPage",
    components: {
        PokemonOptions,
        PokemonPicture,
    },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: "",
        };
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions();

            const rndInt = Math.floor(Math.random() * 4);
            this.pokemon = this.pokemonArr[rndInt];
        },
        checkAnswer(selectedId) {
            this.showPokemon = true;
            this.showAnswer = true;
            if (selectedId == this.pokemon.id)
                this.message = `Correcto, ${this.pokemon.name}`;
            else this.message = `Ups!, era ${this.pokemon.name}`;
        },
        newGame() {
            this.showPokemon = false;
            this.showAnswer = false;
            this.pokemonArr = [];
            this.pokemon = null;
            this.mixPokemonArray();
        },
    },
    mounted() {
        this.mixPokemonArray();
    },
};
</script>
