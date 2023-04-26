<template>
    <button @click="getBack">Regresar</button>
  <div class="container form-group">
    <form class="form" @submit.prevent="handleSubmit">
      <h1 class="form-title">Insertar</h1>
      <p v-if="message" value>{{ message }}</p>
      <div class="form-group">
        <input
          class="form-input"
          id="ncodigo"
          v-model="ncodigo"
          placeholder="Código"
          required
        /><br />
        <input
          class="form-input"
          v-model="nnombre"
          placeholder="Nombre"
          required
        /><br />
        <button type="submit" class="form-button" @click="agregarCosto">
          Agregar
        </button>
      </div>
    </form>
  </div>
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
    (this.ncodigo = ""), (this.nnombre = "");
  },
  methods: {
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
    getBack(){
        this.$router.push({ path: "cenCosto" });
    }
  },
};
</script>
<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.form {
  width: 90%;
  max-width: 400px;
  padding: 30px;
  border-radius: 5px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
}

.form-title {
  text-align: center;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 20px;
  margin-right: 10px;
  
}

.form-label {
  display: block;
  margin-bottom: 5px;
}

.form-input {
  display: block;
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  margin: 0px 20px 0px 0px ; 
}

.form-button {
  display: block;
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: #333;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.form-button:hover {
  background-color: #444;
}
</style>
