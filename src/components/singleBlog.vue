<template>
  <div id="single-blog">
    <h1 class="fadeIn">{{blog.title | toUppercase}}</h1>
    <article>{{blog.content}}</article>
    <p><span class="bolder"> Author: </span> {{blog.author}}</p>
    <p class="bolder">Categories:</p>

    <p v-for="category in blog.categories">{{category}}</p>

  </div>
</template>

<script>
  export default {
    data() {
      return{
        id:this.$route.params.id,
        blog: {}
      }
    },
    filters:{
      'to-uppercase': function(value){
        return value.toUpperCase();
      },
      toUppercase(value){ //works the same as before just a little neater
        return value.toUpperCase();
      }
    },
    created(){

      this.$http.get('https://vue-playlist-9b0d2.firebaseio.com/posts/' + this.id +'.json')
        .then(function(data){
          return data.json();
        }).then(function(data){
        this.blog = data;
      });
    }
  }
</script>
<style>
  .bolder{
    font-weight: 600;
  }
  #single-blog{
    float: left;
    width: 90%;
    margin: 0 auto;
    padding: 0 5% 0 5%;
    margin-bottom: 200px;
  }

</style>
