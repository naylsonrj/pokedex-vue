<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div id="pokemon">
    <div class="card">
        <!-- <div class="card-image ">
        <figure class="media-center">
          <img :src="pokemon.other"  alt="Pokedex API">
        </figure>
      </div> -->
      <!-- <div class="card-content is-align-content-center  ">
        <div class="media">
          <div class="media-left">
            <figure class="image is-128x128">
              <img :src="pokemon.other" />
            </figure>
          </div>
          <div class="media-content ">
            <p class="title ">{{ num }} - {{ name | uppercase }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>
      </div> -->

    <div class="table-container">
      <table class="table">
        <thead>
          <tr>
            <th>Height</th>
            <th>Weight</th>
            <th>name</th>
            <th>type</th>
            <th>abilities</th>
          </tr>

        </thead>
        
        <tbody>
          <tr>
            <td>
              <figure class="image is-68x68">
              <img :src="pokemon.front" />
            </figure>
            </td>
            <td>
              <figure class="image is-68x68">
              <img :src="pokemon.back" />
            </figure>
            </td>
             <td>{{ pokemon.name }}</td>
             <td>{{ pokemon.type }}</td>
            <td>{{ pokemon.abilities }}</td>
          </tr>
        </tbody>

      </table>
    </div>




    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.pokemon.other = res.data.sprites.other.dream_world.front_default;
        this.pokemon.name = res.data.name;
        this.pokemon.abilities = res.data.abilities[0].ability.name; 
      })
      .catch((error) => {
        console.log(error);
      });
  },
  data() {
    return {
      pokemon: {
        type: "",
        front: "",
        back: "",
        other: "",
        name: "",
        abilities: [],
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  filters: {
    uppercase: function (value) {
      if (!value) return "";
      value = value.toString();
      return value.toUpperCase();
    },
  },
};
</script>

<style>
#pokemon {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
</style>