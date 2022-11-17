<template>
  <div v-if="listaFavoritos.length != 0">
    <button
      @click="mostrarFavorito = true"
      class="py-2 px-4 bg-green-500 text-white font-semibold rounded-lg shadow-md hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-green-400 focus:ring-opacity-75"
    >
      Mostrar Favoritos
    </button>
    <div id="resultado" v-if="mostrarFavorito">
      <br />
      <h1 class="font-sans md:font-serif m-2 p-2.5">LISTA DE FAVORITOS</h1>
      <br />
      <ul>
        <li v-for="(personaje, index) in listaFavoritos" v:bin-key="personaje.char_id">
          <img :src="personaje.img" />
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
            @click="eliminar(index)"
            class="py-2 px-4 bg-green-500 text-white font-semibold rounded-lg shadow-md hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-red-400 focus:ring-opacity-75 transition duration-300 ease-in-out"
          >
            Eliminar
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListaFavoritos",
  data() {
    return {
      mostrarFavorito: false,
    };
  },
  props: {
    listaFavoritos: {
      type: Array,
    },
  },
  methods: {
    eliminar(index) {
      for (let i = 0; i < this.listaFavoritos.length; i++) {
        if (this.listaFavoritos[i] === index) {
          this.listaFavoritos.splice(index, 1);
        }
      }
    },
  },
};
</script>

<style scoped>
ul li img {
  width: 450px;
  height: 600px;
  margin: 5px;
  border: 4px solid;
}

#resultado img {
  display: flex;
  flex-wrap: wrap;
  margin: 5px;
  padding: 5px;
}
</style>
