<template>
  <BuscarPersonaje @BuscarPersonaje="getPersonajes($event)" />
  <div id="container">
    <div v-for="personaje in filtered">
      <img :src="personaje.img" /> <br />
      <h1>
        <u
          ><b>{{ personaje.name }}</b></u
        >
      </h1>
      <p><b>Fecha de nacimiento:</b> {{ personaje.birthday }}</p>
      <p><b>Alias:</b> {{ personaje.nickname }}</p>
      <p>
        <b>Trabajo:</b>
        {{ personaje.occupation[0] }} <br />
        {{ personaje.occupation[1] }}
      </p>
      <button
        @click="añadirFavorito(personaje)"
        class="focus:outline-black bg-purple-600 bg-opacity-75 bg-red-500 hover:bg-red-700 rounded-lg"
      >
        Add Favorite
      </button>
    </div>
  </div>
  <ListaFavoritos :listaFavoritos="listaPersonajesFavoritos" />
</template>

<script>
import axios from "axios";
import BuscarPersonaje from "./components/BuscarPersonaje.vue";
import ListaFavoritos from "./components/ListaFavoritos.vue";

export default {
  name: "App",
  components: {
    BuscarPersonaje,
    ListaFavoritos,
  },
  data() {
    return {
      listaPersonajes: [],
      resultadoDevuelto: "",
      listaPersonajesFavoritos: [],
    };
  },
  methods: {
    getPersonajes(data) {
      this.resultadoDevuelto = data;
      axios.get("https://breakingbadapi.com/api/characters").then((response) => {
        this.listaPersonajes = response.data;
      });
    },
    añadirFavorito(personaje) {
      if (this.listaPersonajesFavoritos.length != 0) {
        if (!this.listaPersonajesFavoritos.includes(personaje)) {
          this.listaPersonajesFavoritos.push(personaje);
        } else {
          console.log("error, ya está añadido");
        }
      } else {
        this.listaPersonajesFavoritos.push(personaje);
      }
    },
  },

  computed: {
    filtered() {
      return this.listaPersonajes.filter((el) => {
        return el.name.toLowerCase().includes(this.resultadoDevuelto.toLowerCase());
      });
    },
  },
};
</script>

<style scoped>
#container {
  display: flex;
  flex-wrap: wrap;
  margin: 5px;
  padding: 5px;
}

#container img {
  width: 450px;
  height: 600px;
  margin: 5px;
  border: 4px solid;
}

#container h1 {
  justify-content: center;
}
</style>
