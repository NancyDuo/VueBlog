<template>
  <h1 v-show = "logout">
      You have logged out!
  </h1>
</template>

<script>
import axios from 'axios'
//import store from '../store/index'
export default {
    name:'Logout',
    data() {
        return {
            logout:false
        }
    },
    mounted(){
         console.log('i am in')
        axios({
                method:'post',
                url:'http://localhost:3000/logout',
                //data:qs.stringify(this.loginDatail)   
            }).then((res)=>{
                if(res.data==='logout'){
                    console.log('i did lout')
                    this.logout = true
                    this.$store.commit('LOGOUT')
                    setTimeout(()=>{this.$router.push('/home')},2000)    
                }else{
                    alert('canot logout')
                }   
            })
    
    }
      
}
</script>

<style>

</style>