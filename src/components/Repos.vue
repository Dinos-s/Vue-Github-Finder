<template>
    <div>
        <h2>Reposijtorios de {{ user }}:</h2>
        <ul>
            <li v-show="vazio">Sem repositórios</li>
            <li v-for="repo in repos">
                <h4>{{ repo.name }}</h4>
                <p>{{ repo.description }}</p> 
                <p>{{ repo.language }}</p>
                <a :href="repo.html_url">🔗{{ repo.html_url }}</a>
            </li>
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

<style scoped>
h2{
    color: #fff;
}

ul {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-evenly;
}

li {
    list-style: none;
    background: white;
    border-radius: 10px;
    margin: 12px 4px;
    padding: 5px;
    width: 410px;
    height: auto;
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.466);
}

li h4 {
    text-align: center;
    margin-bottom: .4rem;
}

li p {
    margin-bottom: 4px;
}

a{
    text-decoration: none;
    cursor: pointer;
    color: #7447bc;
}
</style>