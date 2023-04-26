<template>
  <div class="form-group">
    <form class="login-form" @submit.prevent="handleSubmit">
      <h1>Insertar</h1>
      <p v-if="message" value>{{ message }}</p>
      <input id="ncodigo" v-model="ncodigo" placeholder="Código" required />
      <input v-model="nnombre" placeholder="Nombre" required />
      <button type="submit" class="form-button" @click="agregarCosto">
        Agregar
      </button>
    </form>
  </div>
  <div class="container">
    <h1>Lista de costos</h1>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Editar</th>
          <th>Eliminar</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(costo, index) in costos" :key="index">
          <td>{{ costo.Codigo }}</td>
          <td>{{ costo.NombreCentroCostos }}</td>
          <td><button @click="editarCosto(index)">Editar</button></td>
          <td><button @click="eliminarCosto(index)">Eliminar</button></td>
        </tr>
      </tbody>
    </table>
  </div>
  <hr />
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      costos: "",
      message: "",
      ncodigo: "",
      nnombre: "",
    };
  },
  mounted() {
    this.message = "";
    (this.ncodigo = ""), (this.nnombre = ""), this.obtenerCosto();
  },
  methods: {
    async obtenerCosto() {
      this.message = "";
      let url = "http://localhost:8000/api/getCentrosCostos/";
      const { data } = await axios.get(url);
      this.costos = data;
    },

    async agregarCosto() {
      this.message = "";
      let formData = {
        codigocentrocostos: this.ncodigo,
        descripcioncentrocostos: this.nnombre,
      };
      let url = "http://localhost:8000/api/insertCentrosCostos/";
      const { data } = await axios({
        method: "post",
        url: url,
        data: formData,
      });
      this.message = data.message;
      this.obtenerCosto();
    },

    async editarCosto(index) {
      const costoEditado = prompt("Editar costo", this.costos[index].NombreCentroCostos);
      if (costoEditado !== null) {
        this.message = "";
        let formData = {
          codigocentrocostos: this.costos[index].Codigo,
          descripcioncentrocostos: costoEditado,
        };
        let url = "http://localhost:8000/api/updateCentrosCostos/";
        const { data } = await axios({
          method: "post",
          url: url,
          data: formData,
        });
        this.obtenerCosto(); 
      }
    },
    async eliminarCosto(index) {
      if (confirm("¿Eliminar costo?")) {
        this.message = "";
        let formData = {
          codigocentrocostos: this.costos[index].Codigo,
          descripcioncentrocostos: this.costos[index].NombreCentroCostos,
        };
        let url = "http://localhost:8000/api/deleteCentrosCostos/";
        const { data } = await axios({
          method: "post",
          url: url,
          data: formData,
        });
        this.obtenerCosto();
      }
    },
  },
};
</script>
<style>
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>
