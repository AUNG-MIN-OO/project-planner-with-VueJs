<template>
    <div class="card">
        <div class="card-body">
            <h1 class="text-center fw-bolder">Create Project</h1>
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
                <button class="btn float-end">Add</button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            title:"",
            detail:""
        }
    },
    methods:{
        addProject(){
            fetch("http://localhost:3000/projects",{
                method:"POST",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail,
                        complete:false
                    }
                )
            })
            .then(()=>{
                // redirect
                this.$router.push("/");
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>
    .btn{
        background-color: #ba53de;
        padding: 10px 30px;
        color: white;
        font-weight: bold;
    }
</style>