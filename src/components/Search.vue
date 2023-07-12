<template>
    <div>
        <div class="search">
            <input type="text" v-model="user" placeholder="Nome de um usuário">
            <button @click="pesquisar">pesquisar</button>
        </div>
        <h1 v-show="Iserro" class="erro">Usuário não encontrado!</h1>
        <div v-if="data" class="container">
            <h2>{{ data.name }}</h2>
            <p>{{ data.login }}</p>
            <a :href="data.html_url" target="_blank">
                <img :src="data.avatar_url" :alt="data.login">
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
    gap: .8rem;
}

.search input {
    border-radius: 4px;
    border: none;
    width: 190px;
    height: 40px;
    text-align: center;
}

.search button {
    border-radius: 4px;
    border: none;
    cursor: pointer;
    margin-top: 3px;
    width: 133px;
    height: 35px;
    align-items: center;
    justify-content: center;
    background-color: rgb(2, 18, 110);
    color: #fff;
}

.search button:hover {
    background-color: #5591eb;
    transition: 1s;
}

.erro {
    margin: 24px;
    background-color: #c00b0b;
    border-radius: 40px;
}

.container {
    margin-top: 14px; 
    display: flex;
    flex-direction: column;
}

.container img {
    border: solid 2px #55b4eb
}

.container img:hover {
    transition: .1s;
    border: solid 5px #0ee04d
}

.container img,
a {
    border-radius: 50%;
    width: 140px;
}
</style>