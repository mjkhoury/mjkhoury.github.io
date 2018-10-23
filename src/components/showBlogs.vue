
<template>
  <div v-theme="'wide'" id="show-blogs">
    <h1 class="slideRight">All Articles</h1>
    <input id="mySearchBox" type="text" v-model="search" placeholder="Search Articles">
    <p>(Implements Dynamic search using title keywords)</p>
    <div v-for="blog in filteredBlogs" class="single-blog addBorder">
      <router-link v-bind:to="'/blog/'+blog.id"> <h2 class="fadeIn">{{blog.title | toUppercase }}</h2> </router-link>
      <article>{{blog.content.slice(0,600) + '...'}}</article>
      <router-link v-bind:to="'/blog/'+blog.id"> <p id="readMore">Read more</p> </router-link>
    </div>

  </div>
</template>

<script>

  import searchMixin from '../mixins/searchMixin'


  export default {


    data () {
      return {
        blogs:[],
        search: ''
      }
    },
    methods: {

    },
    computed:{

    },
    filters:{
      'to-uppercase': function(value){
        return value.toUpperCase();
      },
      toUppercase(value){ //works the same as before just a little neater
        return value.toUpperCase();
      }
    },
    directives:{
      'rainbow2': {
        bind(el,binding,vnode){
          el.style.color = "#" + Math.random().toString().slice(2,8);
        }
      }
    },
    mixins: [searchMixin],
    created() {
      this.$http.get('https://vue-playlist-9b0d2.firebaseio.com/posts.json')
        .then(function(data){
          return data.json();
        }).then(function(data){
        var blogsArray =[];
        for (let key in data){
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      })
    }
  }
</script>

<style >
  body{
    margin: 0;

  }
  h2{
    text-decoration: none;
    color:rgba(0,0,0,0.7);
  }

  #show-blogs{
    float:left;
    width:90%;
    margin:0 auto;
    padding:0 5% 0 5%;
    margin-bottom:200px;

  }
  .single-blog{
    padding:20px 0;
    margin: 20px 0;
    box-sizing: border-box;
    border-top: 2px solid rgba(0,0,0,0.5);

  // border-bottom: 3px solid rgba(0,0,0,0.5);
  }
  #mySearchBox {
    border: 1px solid rgba(255,190,100,0.90);
    border-radius: 4px;
    cursor: pointer;
    outline:none;
    width:320px;
    padding:3px;

  }
  #mySearchBox:focus {
    background-color:rgba(0,0,0,0.04);
    border-color: rgba(0,0,0,0.4);
  }
  #readMore{
    display:inline-block;
    color: rgba(255,190,100,1);
    border-top:1px solid rgba(0,0,0,0);
    border-bottom:1px solid rgba(0,0,0,0);
  }
  #readMore:hover{
    border-top:1px solid rgba(0,0,0,0.5);
    border-bottom:1px solid rgba(0,0,0,0.5);
    color: rgba(255,190,100,0.5);
  }
  .fadeIn{
    opacity:0;
    -webkit-animation-name: fadeIn;
    -moz-animation-name: fadeIn;
    -o-animation-name: fadeIn;
    animation-name: fadeIn;
    -webkit-animation-duration: 2s;
    -moz-animation-duration: 2s;
    -o-animation-duration: 2s;
    animation-duration: 2s;
    -webkit-animation-fill-mode: forwards;
    -moz-animation-fill-mode: forwards;
    -o-animation-fill-mode: forwards;
    animation-fill-mode: forwards;
  }

  @-webkit-keyframes fadeIn {
    0% {
      opacity:0;

    }
    100% {
      opacity:1;

    }
  }
  @keyframes fadeIn {
    0% {
      opacity:0;

    }

    100% {
      opacity:1;

    }
  }
  .slideRight{

    -webkit-animation-name: slideRight;
    -moz-animation-name: slideRight;
    -o-animation-name: slideRight;
    animation-name: slideRight;
    -webkit-animation-duration: 1s;
    -moz-animation-duration: 1s;
    -o-animation-duration: 1s;
    animation-duration: 1s;
    -webkit-animation-fill-mode: forwards;
    -moz-animation-fill-mode: forwards;
    -o-animation-fill-mode: forwards;
    animation-fill-mode: forwards;
  }

  @-webkit-keyframes slideRight {
    0% {
      margin-left:-10%;

    }
    100% {
      margin-left:0;

    }
  }
  @keyframes slideRight {
    0% {
      margin-left:-10%;

    }
    100% {
      margin-left:0;

    }
  }

  .addBorder{
    border-top: 0px solid rgba(0,0,0,0.0);

    -webkit-animation-name: addBorder;
    -moz-animation-name: addBorder;
    -o-animation-name: addBorder;
    animation-name: addBorder;
    -webkit-animation-duration: 2s;
    -moz-animation-duration: 2s;
    -o-animation-duration: 2s;
    animation-duration: 2s;
    -webkit-animation-fill-mode: forwards;
    -moz-animation-fill-mode: forwards;
    -o-animation-fill-mode: forwards;
    animation-fill-mode: forwards;
    -webkit-animation-delay: 1s;
    -moz-animation-delay: 1s;
    -o-animation-delay: 1s;
    animation-delay: 1s;
  }

  @-webkit-keyframes addBorder {
    0% {
      border-top: 0px solid rgba(0,0,0,0.0);

    }
    100% {
      border-top: 2px solid rgba(0,0,0,0.5);

    }
  }
  @keyframes addBorder {
    0% {
      border-top: 0px solid rgba(0,0,0,0.0);

    }
    100% {
      border-top: 2px solid rgba(0,0,0,0.5);

    }
  }
</style>
