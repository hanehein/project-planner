<template>
    <h1>Edit Project {{id}}</h1>
    <form action="" @submit.prevent="addProject">
        <label for="">Project Title</label>
        <input type="text" v-model="title">
        <label for="">Project Detail</label>
        <input type="text" v-model="detail">

        <button @click="editProject">Edit Project</button>
    </form>
</template>

<script>
export default {
    props:["id"],

    data(){
        return{
            title: "",
            detail: ""
        }
    },

    mounted(){
        fetch("http://localhost:3000/projects/" + this.id)
        .then((resol)=>{
            return resol.json();
        })
        .then((data)=>{
            this.title = data.title
            this.detail = data.detail
        })
        .catch((err)=>{
            console.log(err);
        })
    },

    methods:{
        editProject(){
            fetch("http://localhost:3000/projects/" + this.id,{
                method:"PATCH",
                headers:{
                    "Content-type":"application/json"
                },
                body:JSON.stringify({
                    title:this.title,
                    detail:this.detail
                })
            })
            .then(()=>{
                this.$router.push('/')
            })
            .catch((err)=>{
                console.log(err);
            })
            
        }
    }
}
</script>

<style>

</style>