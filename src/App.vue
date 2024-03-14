<template>
  <!-- Header -->
  <div class="header">
    <h1>
      <i :class="shoppingIcon">local_mall</i>{{ header }}
    </h1>
    <button v-if="!showForm" class="btn btn-primary" @click="showForm = true">Agregar Articulo</button>
    <button v-if="showForm" class="btn" @click="cancelAddItem">Cancelar</button>
  </div>
  <!-- Formulario -->
  <form v-if="showForm" v-on ="saveItems" class="add-item form">
    <input v-model="newItem" type="text" placeholder="Agregar Articulos">
    <!-- Checkbox -->
    <label>
      <input type="checkbox" v-model="newItemHighPriority"> 
      Alta Prioridad 
    </label>
    <!-- Boton -->
    <button class="btn btn-primary">Agregar Articulo</button>
  </form>
  <!-- Entrega de lista -->
  <ul>
    <li v-for="{ id, label } in items" :key="id">⭐ {{ label }} </li>
  </ul>
  <!-- Mensaje condicional -->
  <p v-if="items.length === 0">🥀 No hay elementos en la lista 🥀</p>
</template>

<script setup>
import { ref } from 'vue'

const header = ref(' App lista de compras');
const shoppingIcon = ref('material-icons shopping-cart-icon');
const items = ref([]);
const newItem = ref('');
const newItemHighPriority = ref(false);
const showForm = ref(false);

const saveItems = () => {
  items.value.push({ id: items.value.length, label: newItem.value });
  newItem.value = "";
};

const cancelAddItem = () => {
  showForm.value = false;
};
</script>

<style scoped>
.shopping-cart-icon { font-size: 2rem; }
</style>
