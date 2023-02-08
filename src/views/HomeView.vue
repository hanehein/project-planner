<template>
  <div class="home">
    <h1>Home Page</h1>
      <Filternav @filterValue= "current = $event" :current= "current" ></Filternav>
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete = "deleteProject" @complete="completeProject"></SingleProject>
      </div>     
  </div>
</template>




<script>
import Filternav from '../components/Filternav'
import SingleProject from '../components/SingleProject'
export default {
  name: 'HomeView',
  components: {
    Filternav,
    SingleProject,
  },

  data(){
    return{
      projects:[],
      current:"all"
    }
  },

  methods:{
    deleteProject(id){
      this.projects=this.projects.filter(project=>{
        return project.id != id
      })
    },

    completeProject(id){
      let findProject = this.projects.find(project=>{
        return project.id === id
      });
      findProject.complete = !findProject.complete
    }
  },
   
  mounted(){
    fetch("http://localhost:3000/projects")
    .then((response)=>{
      return response.json()
    })
    .then((datas)=>{
      this.projects=datas
    })
    .catch(()=>{

    })
  }
}
</script>
