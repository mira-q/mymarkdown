<template>
  <div id="app">
<Home v-if="!isLogin"></Home>
<Myapp v-if="isLogin" :user="userData"></Myapp>
  </div>
</template>

<script>
import Home from "./components/Home.vue"
import Myapp from "./components/Myapp.vue"

export default {
  name: 'app',
  data () {
    return {
      isLogin: false,
      userData: null
    }
  },
  components:{
    Home: Home,
    Myapp: Myapp
  },
  created: function(){
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);
      if(user){
        this.isLogin = true;
        this.userData = user;
      }
      else{
        this.isLogin = false;
        this.userData = null;
      }
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
