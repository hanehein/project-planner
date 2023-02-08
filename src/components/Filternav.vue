<template>
  <nav class="filter-nav">
    <button @click="filterby('all')" :class= "{active : current === 'all'}">All</button>
    <button @click="filterby('complete')" :class= "{active : current === 'complete'}">Complete</button>
    <button @click="filterby('ongoing')" :class= "{active : current === 'ongoing'}">Ongoing</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods:{
        filterby(value){
            // console.log(value);
            this.$emit("filterValue",value)
        }
    }
}
</script>

<style>
    .filter-nav button{
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        font-size: 12px;
        text-transform: uppercase;
        cursor: pointer;
        margin-right: 10px;
        letter-spacing: 1px;
        font-weight: bold;
    }

    button.active{
        color: #333;
    }
</style>