<template>
    <div>
        <div class="search">
            <input type="text" v-model="user" placeholder="Nome de um usuário">
            <button @click="pesquisar">pesquisar</button>
        </div>
        <h1 v-show="Iserro">Usuário não encontrado!</h1>
        <div v-if="data" class="container">
            <h2>{{ data.name }}</h2>
            <p>{{ data.login }}</p>
            <a :href="data.html_url" target="_blank">
                <img :src="data.avatar_url" :alt="data.login" >
            </a>
        </div>
        <Repos v-if="data" :user="data.login" />
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
                    console.log(res);
                    this.Iserro = false;
                })
                .catch(erro => {
                    if (erro.response.status === 404) {
                        this.Iserro = true;
                        this.data = null
                    }
                });
            this.user = "";
        },
        repos(user) {
            this.user = user;
        }
    },
    components: { Repos }
}
</script>

<style>
.search {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: .6rem;
}

.search input {
    border-radius: 4px;
    border: none;
    text-align: center;
}

.search button {
    border-radius: 4px;
    border: none;
    cursor: pointer;
}

.container {
    display: flex;
    flex-direction: column;
}

.container img, a {
    border-radius: 50%;
    width: 140px;
}
</style>