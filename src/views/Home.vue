<template>
  <div class="home">
    <h1 class="text-uppercase">Home</h1>
    <FilterNav @filteredValue="current=$event" :current="current"></FilterNav>
    <div v-for="project in projects" :key="project.id" >
      <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"></SingleProject>
    </div>
  </div>
 </template>

<script>


import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
  name:'Home',
  components: {
    FilterNav,
    SingleProject,
  },
  data(){
    return{
      projects:[],
      current:"all",//fileteredValue from filterNav.vue
    }
  },
  methods:{
    deleteProject(id){
      this.projects=this.projects.filter(project=>{
        return project.id!=id;
      })
    },
    completeProject(id){
      let findProject = this.projects.find(project=>{
        return project.id===id;
      })// we got one object now = {}
      findProject.complete=!findProject.complete
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects")
    .then((response)=>{
      return response.json();
    })
    .then((datas)=>{
      this.projects=datas;
    })
    .catch((err)=>{

    })
  }
}
</script>
<style>
  
</style>
