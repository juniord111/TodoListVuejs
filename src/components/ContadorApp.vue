<template>
 <div>
    <h1>Contador</h1>
    <h2>{{ contadorUser }}</h2>
    <button @click="aumentar">➕ Aumentar</button>
    <button @click="disminuir">➖ Disminuir</button>
    <button @click="resetear">🔄 Resetear</button>
    <ul>
        <li v-for="(valor, index) in historial" :key="index">
            {{ valor }}
        </li>
    </ul>
 </div>
</template>
<script setup>
import { ref } from 'vue';
 let contadorUser = ref(0)
    let historial = ref([])
 function aumentar (){
   contadorUser.value++
   historial.value.push(contadorUser.value)
 }

 function disminuir() {
    contadorUser.value--
    historial.value.push(contadorUser.value)
 }

 function resetear() {
    contadorUser.value = 0
 }
</script>
<style scoped lang="scss">

$color-fondo: #f4f4f4;
$color-texto: #333;
$color-primario: #4caf50;
$color-secundario: #ffffff;
$color-boton-hover: darken($color-primario, 10%);
$color-boton-danger: #e74c3c;
$color-boton-danger-hover: darken($color-boton-danger, 10%);
$fuente-principal: 'Arial', sans-serif;

// 🏗 Estilos generales
body {
  background-color: $color-fondo;
  font-family: $fuente-principal;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

// 📦 Contenedor principal
div {
  background: $color-secundario;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  width: 350px;
  text-align: center;
}

// 📝 Títulos
h1 {
  font-size: 2rem;
  margin-bottom: 10px;
  color: $color-texto;
}

h2 {
  font-size: 3rem;
  margin-bottom: 20px;
  font-weight: bold;
}


button {
  margin: 10px;
  padding: 10px 15px;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  color: white;
  transition: background 0.3s;

  &:nth-child(1) {
    background-color: $color-primario;

    &:hover {
      background-color: $color-boton-hover;
    }
  }

  &:nth-child(2) {
    background-color: #ff9800;

    &:hover {
      background-color: darken(#ff9800, 10%);
    }
  }

  &:nth-child(3) {
    background-color: $color-boton-danger;

    &:hover {
      background-color: $color-boton-danger-hover;
    }
  }
}


ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;

  li {
    background: lighten($color-primario, 35%);
    margin: 5px 0;
    padding: 10px;
    border-radius: 5px;
    color: $color-texto;
    font-weight: bold;
  }
}

</style>