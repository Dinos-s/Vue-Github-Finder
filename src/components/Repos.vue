<template>
    <div>
        <h2>Repositorios de {{ user }}:</h2>
        <ul>
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
            repos: []
        }
    },
    props: {
        user: String,
        required: true,
    },
    methods: {
        RepoUsers(){
            api.get(`/${this.user}/repos`)
            .then(res => {
                console.log(res.data);
                this.repos = res.data
                
            })
            .catch(erro => {
                console.log(erro);
            })
        }
    },
    mounted(){
        this.RepoUsers()
    }
}
</script>