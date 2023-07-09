<template>
    <div>
        <h2>Reposijtorios de {{ user }}:</h2>
        <ul>
            <li v-show="vazio">Sem repositórios</li>
            <li v-for="repo in repos">{{ repo.name }}</li>
        </ul>
    </div>
</template>

<script>
import api from '../services/api';

export default {
    name: 'Repositorios',
    data() {
        return {
            repos: [],
            vazio: false
        }
    },
    props: {
        user: String,
        required: true,
    },
    watch: {
        user: {
            handler() {
              this.RepoUsers()
            }
        }
    },
    methods: {
         RepoUsers() {
            setTimeout(() => {
                 api.get(`/${this.user}/repos`)
                .then(res => {
                    console.log(res.data);
                    this.repos = res.data
                    const repos = res.data
                    if (repos.length === 0) {
                        this.vazio = true
                    } else {
                        this.vazio = false
                    }
                })
                .catch(erro => {
                    console.log(erro);
                })
            }, 500)            
        }
    },
    mounted(){
        this.RepoUsers()
    }
}
</script>

<style>
li {
    list-style: none;
}
</style>