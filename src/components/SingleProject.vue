<template>
  <div class="row">
    <div class="card shadow mb-3 borderLeft" :class="{complete:project.complete}">
      <div class="card-body">
        <div class="d-flex justify-content-between align-items-center">
          <div>
            <h3 class="card-title fw-bold" @click="showDetail=!showDetail">{{project.title}}</h3>
          </div>
          <div class="text-nowrap">
            <span class="material-icons text-danger me-2" @click="deleteProject">delete</span>
            <router-link :to="{name:'EditProject',params:{id:this.project.id}}">
              <span class="material-icons text-warning me-2">edit</span>
            </router-link>
            <span class="material-icons text-success" @click="completeProject">done</span>
          </div>
        </div>
        <h6 v-if="showDetail" class="fw-bold">詳しい説明</h6>
        <p v-if="showDetail">{{project.detail}}</p>
        
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:['project'],
  data(){
    return{
      showDetail:false,
      api:  "http://localhost:3000/projects/",
    }
  },
  methods:{
    deleteProject(){
      let deleteRoute = this.api+this.project.id;
      fetch(deleteRoute,{method:"DELETE"})
      .then(()=>{
        this.$emit("delete",this.project.id)
      })
      .catch((err)=>{
        console.log(err)
      })
    },
    completeProject(){
      let updateCompleteRoute = this.api+this.project.id;
      fetch(updateCompleteRoute,{
        method:"PATCH",
        headers:{
          "Content-Type":"application/json"
        },
        body:JSON.stringify(
          {
            complete:!this.project.complete
          }
        )
      })
      .then(()=>{
        this.$emit("complete",this.project.id);
      })
      .catch((err)=>{
        console.log(err);
      })
    }
  }
}
</script>

<style>
  .card{
    background-color: #74f9ff; 
    color: #ba53de  ;
  }
  .borderLeft{
    border-left: 8px solid red; 
  }
  .card-title{
    cursor: pointer;
  }
  span{
    cursor: pointer;
    transition: 0.3s;
  }
  span:hover{
    transform: scale(1.3);
  }
  .complete{
    border-left: 8px solid #0abf53;
  }
</style>