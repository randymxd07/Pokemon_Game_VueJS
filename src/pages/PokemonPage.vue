<template>
    <h1 v-if="!pokemon">Espere por favor...</h1>

    <div v-else>
        <h1>¿Quién es este pokémon?</h1>
        
        <PokemonPicture 
            :pokemon-id="pokemon.id" 
            :show-pokemon="showPokemon" 
        />

        <PokemonOptions
            v-if="!showAnswer"
            :pokemons="pokemonArr"
            @selection-pokemon="checkAnswer"
        />

        <template v-if="showAnswer">
            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame" class="custom-btn">
                Nuevo Juego
            </button>
        </template>

    </div>
    
</template>

<script>
import PokemonOptions from '@/components/PokemonOptions'
import PokemonPicture from '@/components/PokemonPicture'

import getPokemonOptions from '@/helpers/getPokemonOptions'


export default {
    components: { PokemonOptions, PokemonPicture },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: ''
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor( Math.random() * 4 )
            this.pokemon = this.pokemonArr[ rndInt ]
        },
        checkAnswer( selectedId ) {
            
            this.showPokemon = true
            this.showAnswer  = true

            if( selectedId === this.pokemon.id ) {
                this.message = `Correcto, ${ this.pokemon.name }`
            } else {
                this.message = `Oops, era ${ this.pokemon.name }`
            }
        },
        newGame() {

            this.showPokemon = false
            this.showAnswer  = false
            this.pokemonArr  = []
            this.pokemon     = null
            this.mixPokemonArray()            

        }
    },
    mounted() {
        this.mixPokemonArray()
    }

}
</script>

<style scoped>

.custom-btn {
    background-color: #ff6363;
    border-radius: 8px;
    border: 1px solid #ff1a1a;
    color: white;
    cursor: pointer;
    padding: 15px;
    text-align: center;
    width: 200px;
    max-width: 250px;
    transition: background-color 0.3s;
    box-sizing: border-box;
}

.custom-btn:hover {
  background-color: #ff1a1a;
}

</style>