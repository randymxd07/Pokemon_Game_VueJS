<template>
  <div class="options-container">
    <ul>
      <li v-for="pokemon in pokemons" 
          :key="pokemon.id"
          @click="$emit( 'selectionPokemon', pokemon.id )">
          {{ pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: {
      type: Array,
      required: true
    }
  },
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  background-color: #ff6363;
  border-radius: 8px;
  border: 1px solid #ff1a1a;
  color: white;
  cursor: pointer;
  margin-bottom: 10px;
  padding: 25px;
  text-align: center;
  width: 200px;
  max-width: 200px;
  transition: background-color 0.3s;
  box-sizing: border-box;
}

li:hover {
  background-color: #ff1a1a;
}

@media screen and (min-width: 768px) {
  li {
    width: 46%;
    display: inline-block;
    margin-right: 4%;
  }
}

.options-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}
</style>