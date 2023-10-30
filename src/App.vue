<template>
        
    <header>
       <div class="wrapper">

        <div @click="toggleActive" id="toggler-icon">
            <span></span>
            <span></span>
            <span></span>
        </div>

        <ul id="nav" :class="activeClass">
            <li><router-link to="/" class="text-dark nav-link">Home</router-link></li>
            <li><router-link to="/about" class="text-dark nav-link">About</router-link></li>
            <li><a href="">Contact</a></li>
        </ul>

       </div>
    </header>

  <router-view/>

  
</template>

<style>
/* #app { */
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; */
/* 
  min-height: 90vh;
} */

/*
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
} */
</style>

<script>
  export default{

    data: function(){
      return {
        active: false,
      }
    },

    methods: {
      toggleActive: function(){
        this.active = !this.active;
      }
    },

    computed: { 
      activeClass: function(){
        if (this.active) return "active";
        else return "";
      }
    }
  }
</script>
