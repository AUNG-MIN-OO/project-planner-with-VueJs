<template>
  <nav>
      <button @click="filterBy('all')" :class="{active : current==='all'}">All</button>
      <button @click="filterBy('complete')" :class="{active : current==='complete'}">Complete</button>
      <button @click="filterBy('ongoing')" :class="{active : current==='ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods:{
        filterBy(value){
            this.$emit("filteredValue",value)
        }
    }
}
</script>

<style scoped>
    button{
        padding: 2px 0;
        margin-right: 30px;
        margin-bottom: 30px;
        border: none;
        color: #00e0ff;
        font-weight: bold;
        transition: 0.4s;
        cursor: pointer;
        background-color: #e8ffe8;
    }
    button:hover{
        transform: scale(1.1);
    }
    .active{
        border-top: 4px solid #ba53de;
    }
</style>