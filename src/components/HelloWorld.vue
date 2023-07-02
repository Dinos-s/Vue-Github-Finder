<template>
  <div>
    <h1>Testando a api do Github</h1>
    <input type="text" v-model="user">
    <button @click="pesquisar()">pesquisar</button>
    <h1 v-show="Iserro">Usuário não encontrado!</h1>
    <div v-if="data">
      <h2>{{ data.login }}</h2>
      <p>{{ data.name }}</p>
      <img :src="data.avatar_url" :alt="data.login">
    </div>
  </div>
</template>

<script>
import api from "../services/api";

export default {
    name: "HelloWorld",
    data() {
        return {
            user: '',
            data: null,
            Iserro: false
        };
    },
    methods: {
        pesquisar() {
            api.get(`/${this.user}`)
                .then(res => {
                this.data = res.data;
                this.Iserro = false;
            })
                .catch(erro => {
                if (erro.response.status === 404) {
                    this.Iserro = true;
                }
            });
            this.user = "";
        }
    }
}
</script>

<style scoped></style>
