<template>
    <div class="container ">
      <h1>Lista de costos</h1>
      <ul>
        <li v-for="(costo, index) in costos" :key="index">
          {{ costo.codigo }} - {{ costo.nombre }}
          <button @click="editarCosto(index)">Editar</button>
          <button @click="eliminarCosto(index)">Eliminar</button>
        </li>
      </ul>
      <form @submit.prevent="agregarCosto">
        <input v-model="nuevoCosto.codigo" placeholder="Código" />
        <input v-model="nuevoCosto.nombre" placeholder="Nombre" />
        <button type="submit">Agregar costo</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        costos: [
          { codigo: "001", nombre: "Costo 1" },
          { codigo: "002", nombre: "Costo 2" },
          { codigo: "003", nombre: "Costo 3" },
        ],
        nuevoCosto: {
          codigo: "",
          nombre: "",
        },
      };
    },
    methods: {
      agregarCosto() {
        this.costos.push({
          codigo: this.nuevoCosto.codigo,
          nombre: this.nuevoCosto.nombre,
        });
        this.nuevoCosto.codigo = "";
        this.nuevoCosto.nombre = "";
      },
      editarCosto(index) {
        const costoEditado = prompt("Editar costo", this.costos[index].nombre);
        if (costoEditado !== null) {
          this.costos.splice(index, 1, {
            codigo: this.costos[index].codigo,
            nombre: costoEditado,
          });
        }
      },
      eliminarCosto(index) {
        if (confirm("¿Eliminar costo?")) {
          this.costos.splice(index, 1);
        }
      },
    },
  };
  </script>

  