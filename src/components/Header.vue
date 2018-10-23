
<template>
  <header >
    <nav >
      <ul id="header" class="header">
        <li><router-link to="/" exact>BLOG</router-link></li>
        <li><router-link to="/add" exact>ADD A NEW ARTICLE</router-link></li>

      </ul>
    </nav>
  </header>

</template>

<script>




  var lastKnownScrollY = 0;
  var currentScrollY = 0;
  var ticking = false;
  var idOfHeader = 'header';
  var eleHeader = null;
  const classes = {
    pinned: 'header-pin',
    unpinned: 'header-unpin',
  };
  function onScroll() {
    currentScrollY = window.pageYOffset;
    requestTick();
  }
  function requestTick() {
    if (!ticking) {
      requestAnimationFrame(update);
    }
    ticking = true;
  }
  function update() {
    if (currentScrollY < lastKnownScrollY) {
      pin();
    } else if (currentScrollY > lastKnownScrollY) {
      unpin();
    }
    lastKnownScrollY = currentScrollY;
    ticking = false;
  }
  function pin() {
    if (eleHeader.classList.contains(classes.unpinned)) {
      eleHeader.classList.remove(classes.unpinned);
      eleHeader.classList.add(classes.pinned);
    }
  }
  function unpin() {
    if (eleHeader.classList.contains(classes.pinned) || !eleHeader.classList.contains(classes.unpinned)) {
      eleHeader.classList.remove(classes.pinned);
      eleHeader.classList.add(classes.unpinned);
    }
  }
  window.onload = function() {
    eleHeader = document.getElementById(idOfHeader);
    document.addEventListener('scroll', onScroll, false);
  }




</script>

<style >
  .header{
    transition: transform 0.25s ease-in-out;

    position:fixed;
  }
  .header-unpin{
    /* display: none; */
    transform: translateY(-65px);
  }
  .header-pin{
    /* display: block; */
    transform: translateY(0);
  }

  nav ul{
    width:100%;
    list-style-type: none;
    position:fixed;
    margin: 0 auto;
    background:rgba(0,0,0,0.82);
    border-bottom: 5px solid rgba(0,0,0,0.1);
    border-top: 5px solid rgba(0,0,0,0.1);
    padding:20px 5% 20px 5%;
  }
  li{
    display: inline-block;
    margin: 0 20px 0 0;
  }
  a{
    color: rgba(255,255,255,0.8);
    text-decoration: none;
    padding: 17px 5px 17px 0;

  }
  nav{
    padding: 5px 0 1px 0;
    margin-bottom: 90px;
    transition: top 0.2s ease-in-out;
  }
  .router-link-active{
    border-top:1px solid rgba(255,255,255,0.2);
    border-bottom:1px solid rgba(255,255,255,0.2);
    color: rgba(255,190,100,0.90);
  }
  a:hover{
    border-top:1px solid rgba(255,255,255,0.5);
    border-bottom:1px solid rgba(255,255,255,0.5);
  }
  .nav-up {
    top: -40px;
  }

</style>
