
<template>
  <div v-theme="'wide'" id="show-blogs">
    <h1> List blog articles</h1>
    <input type="text" v-model="search" placeholder="Search Blogs">
    <div v-for="blog in filteredBlogs" class="single-blog">
      <h2 v-rainbow2>{{blog.title | toUppercase }}</h2>
      <article>{{blog.body | snippet}}</article>
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
      this.$http.get('https://jsonplaceholder.typicode.com/todos/1/posts')
        .then(function(data){
          console.log(data);
          this.blogs = data.body.slice(0,10);

        })
    }
  }
</script>

<style >
  body{
    margin: 0;
  }
  #show-blogs{
    max-width: 800px;
    margin:0 auto;
  }
  .single-blog{
    padding:20px;
    margin: 20px 0;
    box-sizing: border-box;
    background:#eee;
  }

</style>
