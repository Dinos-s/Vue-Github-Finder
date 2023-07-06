<template>
    <div>
        <input type="text" v-model="user" placeholder="Nome de um usuário">
        <button @click="pesquisar">pesquisar</button>
        <h1 v-show="Iserro">Usuário não encontrado!</h1>
        <div v-if="data">
            <h2>{{ data.login }}</h2>
            <p>{{ data.name }}</p>
            <img :src="data.avatar_url" :alt="data.login">
        </div>
        <Repos v-if="data" :user="data.login"/>
    </div>
</template>

<script>
import api from "../services/api";
import Repos from "./Repos.vue";

export default {
    name: "Search",
    data() {
        return {
            user: "",
            data: null,
            Iserro: false
        };
    },
    methods: {
        async pesquisar() {
            await api.get(`/${this.user}`)
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
        },
        repos(user){
            this.user = user;
        }
    },
    components: { Repos }
}
</script>