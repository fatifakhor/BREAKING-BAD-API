<template>
  <div class="bg-yellow-400 bg-gradient-to-l md:bg-gradient-to-r">
    <div>
      <img src="../assets/brbad.jpg" />
    </div>

    <div id="PrimerComponente">
      <input
        type="text"
        id="escribirPersonaje"
        v-model="personaje"
        class="input is-rounded"
      />
      <button
        @click="buscarPersonaje"
        type="submit"
        class="bg-green-600 bg-opacity-75 text-white italic py-2 px-4 border border-green-700 rounded"
      >
        Buscar
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "BuscarPersonaje",
  emits: ["BuscarPersonaje"],
  data() {
    return {
      personaje: "",
    };
  },
  methods: {
    buscarPersonaje() {
      this.$emit("BuscarPersonaje", this.personaje);
    },
  },
};
</script>

<style scoped>
/* el scoped es para que se aplique solo al componente*/

#PrimerComponente {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

#escribirPersonaje {
  outline: 2px solid;
  border-radius: 5px;
  width: 15%;
  height: 30px;
  margin: 0.9rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
