<template>
    <div class="project" @click="showDetail=!showDetail">
        <h3>{{project.title}}</h3>
        <p v-if="showDetail">{{project.detail}}</p>
    </div>
</template>


<script>
export default {
    props:['project'],
    data(){
        return{
            showDetail:false
        }
    }
}
</script>

<style>
    .project{
        padding:20px;
        background-color: #f2f2f2;
        cursor: pointer;
        margin: 10px;
    }

    h3{
        color:indigo;
    }
</style>