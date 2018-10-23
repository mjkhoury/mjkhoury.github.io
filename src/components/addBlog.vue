
<template>
  <div id="add-blog">
    <h2 class="slideRight">Add a New Article Post</h2>
    <div v-if="submitted">
      <h3>Thanks for adding your post!</h3>
    </div>
    <form v-if="!submitted">

      <label class="fadeIn">Blog title</label>
      <input type="text" v-model.lazy="blog.title" placeholder="Lazy Preview in the preview field" required>
      <label class="fadeIn">Blog Content</label>
      <textarea v-model="blog.content" required placeholder="Real-time Preview in the preview field"></textarea>
      <div id="checkboxes">
        <label>Ninjas</label>
        <input type="checkbox" value="ninjas" v-model="blog.categories">
        <label>Fighters</label>
        <input type="checkbox" value="fighters" v-model="blog.categories">
        <label>Wrestlers</label>
        <input type="checkbox" value="wrestlers" v-model="blog.categories">
        <label>Boxers</label>
        <input type="checkbox" value="boxers" v-model="blog.categories">
      </div>
      <label>Author</label>
      <select  v-model="blog.author">
        <option v-for="author in authors">{{author}}</option>
      </select>
      <button @click.prevent="post">Add Blog</button>
    </form>
    <div id="preview">
      <h3 style="color:rgba(255,190,100,0.90);">Preview Blog</h3>
      <p><span class="bolder">Blog title:</span> {{blog.title}}</p>
      <p><span class="bolder">Blog content:</span><p>
      {{blog.content}}</p>
      <p><span class="bolder">Blog Categories:</span></p>
      <ul>
        <li v-for="category in blog.categories">{{category}}</li>
      </ul>
      <p><span class="bolder">Author: </span>{{blog.author}}</p>
    </div>
  </div>
</template>

<script>


  export default {

    data () {
      return {
        blog: {
          title: "",
          content: "",
          categories: [],
          Author: ""
        },
        authors: ['The Cupcake','The Master', 'The VUEer','The Optimist'],
        submitted: false
      }
    },
    methods: {
      post: function(){
        this.$http.post('https://vue-playlist-9b0d2.firebaseio.com/posts.json', this.blog)
          .then(function(data){
            console.log(data);
            this.submitted = true;
          });

      }
    }
  }
</script>

<style>
  #add-blog *{
    box-sizing: border-box;
  }
  #add-blog{
    float: left;
    width: 90%;
    margin: 0 auto;
    padding: 0 5% 0 5%;
    margin-bottom: 200px;
  }
  label{
    display: block;
    margin: 20px 0 10px;
  }
  input[type="text"], textarea{
    display: block;
    width: 100%;
    padding: 8px;
  }
  #preview{
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
  }
  h3{
    margin-top: 10px;
  }
  #checkboxes input{
    display:inline-block;
    margin-right:10px;
  }
  #checkboxes label{
    display:inline-block;

  }
  body{
    margin: 0 auto;
  }
  input[type="text"], textarea  {
    border: 1px solid rgba(255,190,100,0.90);
    border-radius: 4px;
    cursor: pointer;
    outline:none;
    width:320px;
    padding:3px;

  }
  input[type="text"]:focus,  textarea:focus {
    background-color:rgba(0,0,0,0.04);
    border-color: rgba(0,0,0,0.4);
  }
  .bolder{
    font-weight: 600;
  }
</style>
