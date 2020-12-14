<template>
  <div class="home">
      <h1>Home</h1>
      <FilterNav @filterValue="current=$event" :current="current"></FilterNav>
      <div v-for="project in filteredProjects" :key="project.id" >
         <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"></SingleProject>
      </div>
  </div>
      {{current}}
</template>

<script>

import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
  name: 'Home',
  components: {
    FilterNav,
    SingleProject, 
  },
  data(){
    return{
      projects:[], //[{…}, {…}, {…}]
      current:"all"//ongoing complete
    }
  },
  methods:{
    deleteProject(id){
      this.projects=this.projects.filter(project=>{
        return project.id!=id;
      })
    },
    completeProject(id){
        let findProject=this.projects.find(project=>{
          return project.id===id;
        });// {}
        findProject.complete=!findProject.complete
    }
  },
  computed:{
      filteredProjects(){
         if(this.current==="complete"){
           return this.projects.filter((p)=>{
             return p.complete
           })
         }
         if(this.current==="ongoing"){
          return this.projects.filter((p)=>{
             return !p.complete
           })
         }
         return this.projects;
      }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
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
