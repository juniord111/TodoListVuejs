<template>
  <div>
    <h1>Todo List</h1>
    <input v-model="user" type="text">
    <button @click="agregar">Agregar</button>
    <ul>
      <li v-for="item in listaElemento" :key="item.id" :class="{ completado: item.completado }">
        <span>{{ item.contenido }}</span>
        <div class="botones">
          <button @click="completado(item.id)" class="btn-completar">{{ item.completado ? 'Desmarcar' : 'Completar' }}</button>
          <button @click="eliminar(item.id)" class="btn-eliminar">Eliminar</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const user = ref('');
const listaElemento = ref([]);

const agregar = () => {
  if (user.value.trim() === '') return;
  const nuevoElemento = {
    id: Date.now(),
    contenido: user.value,
    completado: false 
  };
  listaElemento.value.push(nuevoElemento);
  user.value = '';
};

const eliminar = (id) => {
  listaElemento.value = listaElemento.value.filter(item => item.id !== id);
};

const completado = (id) => {
  const item = listaElemento.value.find(item => item.id === id);
  if (item) {
    item.completado = !item.completado;
  }
};
</script>

<style lang="scss">
$color-fondo: #0d1117;
$color-primario: #1f6feb;
$color-secundario: #161b22;
$color-texto: #c9d1d9;
$color-boton-hover: lighten($color-primario, 10%);
$color-boton-eliminar: #d73a49;
$color-boton-eliminar-hover: lighten($color-boton-eliminar, 10%);
$fuente-principal: 'Orbitron', sans-serif;

body {
  background-color: $color-fondo;
  font-family: $fuente-principal;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

#app {
  background: $color-secundario;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 0 20px rgba(31, 111, 235, 0.6);
  width: 450px;
  text-align: center;
  border: 2px solid $color-primario;
}

h1 {
  color: $color-primario;
  font-size: 2rem;
  margin-bottom: 20px;
  text-transform: uppercase;
  letter-spacing: 2px;
}

input {
  width: 85%;
  padding: 14px;
  border: 2px solid $color-primario;
  border-radius: 8px;
  outline: none;
  font-size: 1.1rem;
  background: darken($color-secundario, 5%);
  color: $color-texto;
}

button {
  border: none;
  padding: 10px 16px;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s, transform 0.2s;
  font-size: 1rem;
  text-transform: uppercase;
  margin-top: 10px;

  &:hover {
    transform: scale(1.05);
  }
}

.btn-completar {
  background: #2ecc71;
  color: white;
  &:hover {
    background: lighten(#2ecc71, 10%);
  }
}

.btn-eliminar {
  background: $color-boton-eliminar;
  color: white;
  &:hover {
    background: $color-boton-eliminar-hover;
  }
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 25px;

  li {
    background: rgba(31, 111, 235, 0.2);
    margin: 15px 0;
    padding: 14px;
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: $color-texto;
    font-weight: 600;
    box-shadow: 0 4px 10px rgba(31, 111, 235, 0.3);

    .botones {
      display: flex;
      gap: 10px;
    }
  }
}

.completado {
  text-decoration: line-through;
  color: gray;
  background-color: rgba(46, 204, 113, 0.2);
  transition: all 300ms;
}
</style>
