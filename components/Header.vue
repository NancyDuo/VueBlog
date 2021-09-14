<template>
<div class="total">
  <div class="title">Welcome to Nancy's Blog</div>
  <router-link v-if = '!isLogin' class ='login' to ='/login'>Login</router-link>
  <router-link v-else class ='login' to ='/logout'>Logout</router-link>
  <div class="navbar"> 
        <router-link class="rl" to="/home">Home</router-link>
        <router-link class="rl" to="/vue">Vue</router-link>
        <router-link class="rl" to="/database">Database</router-link>
        <router-link class="rl" to= "/axios">Axios</router-link>
        <router-link class="rl" to="/create">Create</router-link>
        
  </div>
  </div>
</template>

<script>
import store from '../store'
export default {
    name:'Header',
    // components:{Login},
    data() {
      return {
       isLogin: false
      }
    },
    mounted() {
      
    },
    methods: {
      forceRerender(){
        this.isLogin = store.state.logined
      }
    },
    watch:{
      '$route'(to, from) {
        if(to.path == '/create'){
          this.forceRerender()
        }
        if(from.path == '/logout'){
          this.forceRerender()
        }
      }
    }

}
</script>

<style scoped lang="less">
.total{
  .title{
  font-size:30px;
  color:white;
  font:bolder;
  text-align: center;
  }
  .login{
  float:right;
  margin-top:-10px;
  margin-bottom:10px;
  margin-right:350px;
  font-size: 15px;
  color:white;
  }
  .navbar{
    width: 100%;
    display: flex;
    justify-content: space-around;
    font-size: 20px;
    .rl{
      padding: 5px;
      text-align: center;
      width: 20%;
      font:bolder;
      color: white;
      border-right: 1px solid rgba(248, 244, 238,0.5);
      background-color: rgba(247, 246, 222, 0.3);
    }
  } 
}
</style>


