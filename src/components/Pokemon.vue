<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div id="pokemon">   


  <div class="card">
    <div class="card-image ">
      <figure class="media-center">
        <img :src="pokemon.other"  alt="Pokedex API">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-left">

          
          <figure class="image is-64x64">
            <img :src="pokemon.back" class="is-rounded"  alt="Pokedex API">
          </figure>
        </div>
        <div class="media-content">
              <p class="title is-4">{{num}} - {{name | uppercase }}</p>
          <p class="subtitle is-6">{{ pokemon.type }}</p>
        </div>
      </div>

 
  </div>
</div>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  created: function(){
    axios.get(this.url).then(res => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.other = res.data.sprites.other.dream_world.front_default;
    }).catch(error => {
      console.log(error);
    });
  }, 
  data() {
    return {
      pokemon: {
        type: '',
        front: '',
        back: ''
      }
    }
  },
    props: {
    num: Number,
    name: String,
    url: String,
    
  }, 
  filters: {
    uppercase: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.toUpperCase()
    }

  }
}
</script>

<style>
  #pokemon {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 40px;
  }
</style>