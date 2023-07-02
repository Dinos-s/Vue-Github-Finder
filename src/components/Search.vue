<template>
    <div>
        <input type="text" v-model="user">
        <button @click="pesquisar()">pesquisar</button>
    </div>
</template>

<script>
export default {
    name: "Search",
    data() {
        return {
            user: ''
        }
    },
    methods: {
        pesquisar(){
            this.$emit('search')
            console.log(user);
        }
    }
}
</script>