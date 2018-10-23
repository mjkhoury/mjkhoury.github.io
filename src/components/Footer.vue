<template>
  <footer>
    <div id="staticFooter">
      <p> &#9400; {{copyright}}  {{title}} <a id="top-arrow" class="top-arrow" v-bind:class="{active: isClicked}" @click="timeOut" href="#top">▲ </a> </p>

    </div>
  </footer>
</template>

<script>

  import { bus } from '../main'

  export default {
    props:{
      title:{
        type: String
      }
    },
    data () {
      return {
        copyright: 'Copyright 2018 MORAD JOSEPH KHOURY',
        arrow: '▲',
        isClicked: false,
      }
    },
    methods:{
      myFilter:function() {
        this.isClicked = !this.isClicked;

      },
      timeOut: function(){
        setTimeout(this.myFilter, 0);
      }
    },
    created() { //fires when the component is created
      bus.$on('titleChangedUsingBus', (data) => {
        this.title = data;
      })
    }
  }
</script>

<style >
  footer{
    width:90%;
    margin-top:220px;

  }
  #staticFooter{
    opacity:0.8;
    width:100%;
    color:rgba(255,255,255,0.9);
  //background:rgba(0,0,0,0.8);
    background-image: url('../assets/4.jpg');
    background-repeat: repeat-x;

    border-top: 5px solid rgba(0,0,0,0.1);
    padding:0 5% 0 5%;
    position:fixed;
    bottom:0;
    margin-top:200px;
  }
  footer p{
    width:90%;
    display:inline-block;
    font-size:14px;
  }

  #top-arrow{
    border:none;
  }
  .top-arrow{
    display:inline-block;
    float: right;
    padding:0;
    font-size:20px;
    border:none;
  }


  .top-arrow.active{
    border:none;
    -webkit-animation: rotate 1s 2;
    -webkit-animation-direction: alternate;
    animation: rotate 1s 2;
    animation-direction: alternate;


  }
  @-webkit-keyframes rotate {
    0% {
      opacity:1;
      color:gold;
    }
    50% {
      opacity:0.5;
      color:gold;
    }
    100% {
      opacity:0;
      color:gold;
    }
  }
  @keyframes rotate {
    0% {
      opacity:1;
      color:gold;
    }
    50% {
      opacity:0.5;
      color:gold;
    }
    100% {
      opacity:0;
      color:gold;
    }
  }
</style>
