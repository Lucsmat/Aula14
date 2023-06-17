<template>
  <div class="about">
    <h1>About</h1>

<div>
  <input type="text" placeholder="Digite o título" v-model="titulo">
</div>
<br/>
<p>{{ titulo }}</p>


    <Propriedade v-bind:titulo="titulo" v-bind:img="estados" />
  </div>
</template>

<script>
import Propriedade from './Propriedade.vue'

export default {
  name: "About",
  components: { Propriedade },
  data() {
    return { titulo: "Aqui é o título",
  estados: [ "SP", "MG", "RJ", "ES"] } 
},
setup() {

  
}
}
</script>