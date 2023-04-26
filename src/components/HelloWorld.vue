<script>
import axios from "axios";
export default {
  data() {
    return {
      username: "",
      password: "",
      emisor: "",
      message: "",
      selected: null,
      comboEmisor: ""
    };
  },
  computed() {},
  mounted() {
    this.message = "";
    this.getComboEmisores();
  },
  methods: {
    async login() {
      this.message = "";
      let formData = {
        nombreUsuario: this.username,
        passwordUsuario: this.password,
        codigoEmisor: this.emisor,
      };
      let url = "http://localhost:8000/api/login/";
      const { data } = await axios({
        method: "post",
        url: url,
        data: formData,
      });
      console.log(data);
      this.getComboEmisores();
      //if(data.success == 1){
      this.message = data.message;
      //}
    },
    async getComboEmisores() {
      let url = "http://localhost:8000/api/getEmisor/";
      const { data } = await axios.get(url);
      this.comboEmisor = data;
    },
  },
};
</script>

<style>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.login-form {
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
  margin-bottom: 10px;
}

.form-label {
  display: block;
  margin-bottom: 5px;
}

.form-input {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
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


<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      You’ve successfully created a project with
      <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>.
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
  