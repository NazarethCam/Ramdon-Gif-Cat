<template>
  <div class="main">
    <h1>Random Gif Cat</h1>
    <div class="contenedor-formulario">
      <div class="formulario">
        <div class="row">
          <label>Titulo:</label>
          <input v-model="formulario.titulo" type="text" />
        </div>
        <div class="row">
          <label>Filtro:</label>
          <select v-model="formulario.filtro">
            <option v-for="filtro in filtros" :key="filtro" :value="filtro">
              {{ filtro }}
            </option>
          </select>
        </div>
        <div class="row">
          <label>Color:</label>
          <select v-model="formulario.color">
            <option
              v-for="(color, index) in colores"
              :key="index"
              :value="color.valor"
            >
              {{ color.nombre }}
            </option>
          </select>
          <div :style="muestraColor" class="circuloColores"></div>
        </div>
        <div class="row">
          <label>Tamaño:</label>
          <input
            @keydown="soloNumeros"
            v-model="formulario.tamano"
            type="number"
          />
        </div>
      </div>
    </div>
    <div class="btn">
      <button @click="crearGatitoChan">Obtener mi gatito</button>
      <img :src="urlGatos" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      colores: [
        { valor: "green", nombre: "Green" },
        { valor: "pink", nombre: "Pink" },
        { valor: "red", nombre: "Red" },
        { valor: "blue", nombre: "BLue" },
        { valor: "yellow", nombre: "Amarillo" },
        { valor: "aqua", nombre: "Agua" },
      ],
      filtros: ["blur", "mono", "sepia", "negative", "paint", "pixel"],

      formulario: {
        titulo: null,
        filtro: "",
        color: "",
        tamano: null,
      },

      urlGatos: "",
    };
  },

  computed: {
    muestraColor() {
      return `background-color: ${this.formulario.color}`;
    },
  },

  methods: {
    soloNumeros(e) {
      if (e.key === "Backspace") {
        return;
      }

      if (!/[0-9]/.test(e.key)) {
        return e.preventDefault();
      }
    },
    crearGatitoChan() {
      this.urlGatos = `https://cataas.com/cat/gif/says/${this.formulario.titulo}?filter=${this.formulario.filtro}&color=${this.formulario.color}&size=${this.formulario.tamano}`;
    },
  },
};
</script>

<style>
:root {
  --text-color: #2c3e50;
  --first-color: lightblue;
  --second-color: lightcoral;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  color: var(--text-color);
}
h1 {
  text-align: center;
  padding-top: 4rem;
  padding-bottom: 4rem;
}
.main {
  width: 100%;
  min-height: 100vh;
  background-color: var(--first-color);
}
.contenedor-formulario {
  background-color: var(--second-color);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.formulario {
  width: 100%;
  padding: 1rem;
  margin: 20px 40%;
}
.row {
  margin: 20px 40%;
  width: 500px;
  padding: 2vh;
  display: flex;
}
.btn {
  padding: 5vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}
button {
  text-align: center;
  padding: 0.2rem 1rem;
  margin-bottom: 1.25rem;
}
section {
  width: 100%;
}
.circuloColores {
  width: 30px;
  height: 30px;
  border: 1px solid black;
  border-radius: 50%;
  margin-left: 0.5rem;
}
</style>