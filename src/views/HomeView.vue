<template>
  <div>
    <h3>Digite o nome da personagem que deseja procurar:</h3>
    <br />
    <input type="text" v-model="nome" @keyup.enter="buscarNome" />


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
  name: "HomeView",
  components: {
    api,
  },

  data() {
    return {
      mostrar: false,
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

