<template>
    <div class="card">
        <div class="card-body">
            <h1 class="text-center fw-bolder">Edit Project</h1>
            <hr>
            <form @submit.prevent="addProject"> 
                <div class="form-group mb-4">
                    <label for="title" class="fs-5 fw-bold mb-2">Project Title</label>
                    <input type="text" id="title" class="form-control" v-model="title">
                </div>
                <div class="form-group mb-4">
                    <label for="detail" class="fs-5 fw-bold mb-2">Project Detail</label>
                    <textarea type="text" id="detail" rows="5" class="form-control" v-model="detail"></textarea>
                </div>
                <hr>
                <button class="btn float-end" @click="updateProject">Update</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    props:["id"],
    data(){
        return{
            title:"",
            detail:"",
            api:"http://localhost:3000/projects/"
        }
    },
    mounted(){
        let apiRoute= this.api+this.id;
        fetch(apiRoute)
        .then((response)=>{
            return response.json()
        })
        .then((datas)=>{
            this.title = datas.title;
            this.detail = datas.detail;
        })
        .catch((err)=>{
            console.log(err)
        })
    },
    methods:{
        updateProject(){
            //fetch api from database
             fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-type":"application/json"
                },
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail
                    }
                )
            })
            .then(()=>{
                this.$router.push('/')
            })
        },
    }
}
</script>

<style>

</style>