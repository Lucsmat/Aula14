<template>
  <div>
    <h1>Lucas Matheus</h1>
    <br />
    <p>Olá mundo</p>
    <input type="checkbox" v-model="ativo" @change="alterar" />
    <br />
    <input type="text" v-model="nome" @keyup.enter="buscarNome" />

    <div v-if="mostrar">
      <h2>Apareceu</h2>
      <ul>
        <li v-for="(item, key) in json" :key="key">
          {{ item }}
        </li>
      </ul>
    </div>

    <div v-for="(item, i) in resultado" :key="i">
      <ul>
        <li>
          <img :src="item.imageUrl" />
          {{ item.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

import api from "../services/api";
import { onMounted, ref } from "vue";

export default {
  name: "PrimeiroComponente",
  components: {
    api,
  },

  data() {
    return {
      ativo: false,
      mostrar: false,
      json: ["Lucas", "Matheus"],
      resultado: "",
    };
  },

  mounted() {
    this.buscar();
  },
  
  methods: {
    alterar() {
      this.mostrar = !this.mostrar;
    },
    buscar() {
      api
        .get("character")
        .then((response) => {
          console.log(response.data.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    buscarNome() {
      api
        .get("character?name=" + this.nome)
        .then((response) => {
          this.resultado = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

