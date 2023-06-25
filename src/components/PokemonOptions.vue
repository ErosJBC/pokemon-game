<template>
    <div class="max-w-screen-lg mx-auto pt-8">
        <div class="grid grid-cols-1 gap-y-2 mx-auto">
            <button
            v-for="pokemon in pokemons"
            :key="pokemon.id"
            @click="$emit('selection', pokemon.id)"
            :disabled="disabled"
            class="bg-violet-600 text-white font-medium rounded py-1 w-[250px] mx-auto hover:bg-violet-800 transition duration-300 disabled:bg-neutral-400"
        >
            {{ pokemon.name }}
        </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        pokemons: {
            type: Array,
            required: true,
        },
        disabled: {
            type: Boolean,
        },
    },
};
</script>
