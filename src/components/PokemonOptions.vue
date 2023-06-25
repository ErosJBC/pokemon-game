<template>
    <div class="options-container">
        <ul>
            <button
                v-for="pokemon in pokemons"
                :key="pokemon.id"
                @click="$emit('selection', pokemon.id)"
                :disabled="disabled"
            >
                {{ pokemon.name }}
            </button>
        </ul>
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
        }
    }
};
</script>

<style scoped>
ul {
    list-style-type: none;
    display: flex;
    flex-direction: column;
}

button {
    background-color: white;
    border-radius: 3px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
    width: 250px;
    padding: 2.5px;
}

button:hover {
    background-color: rgba(0, 0, 0, 0.05);
}

button:disabled {
    background-color: transparent;
    cursor: default;
}

.options-container {
    display: flex;
    justify-content: center;
    margin-top: 0.5rem;
}
</style>
