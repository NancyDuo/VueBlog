<template>
      <form class="login-wrapper">
          <h3>Login</h3>
          <input class = 'login' type="text" placeholder="Email" v-model = "loginDatail.email">
          <input class = 'login' type="text" placeholder="Password" v-model = "loginDatail.password">
          <button class = 'btn' @click.prevent = "login">Login</button>
      </form>
 
</template>

<script>
import axios from 'axios'
import qs from 'querystring'
export default {
    name:'Login',
    data() {
        return {
            loginDatail:{
                email:'',
                password:'',
            },    

        }
    },
    methods: {
        login(){
            axios({
                method:'post',
                url:'http://localhost:3000/login',
                data:qs.stringify(this.loginDatail)   
            }).then((res)=>{
                if(res.data==='findUser'){
                    this.$store.commit('LOGIN')
                    this.$router.push('/create')
                }else{
                    alert('wrong password')
                }   
            })
        }
    }
}
</script>

<style scoped lang = 'less'>
.login-wrapper{
    width: 500px;
    height: 300px;
    margin: 100px auto;
    background-color:white;
    border-radius: 10px;
    box-shadow: 0px 0px 5px rgba(77, 41, 62, 0.932);
    opacity: 90%;
    padding: 20px;
    h3{
    color: rgb(138, 100, 106);

    }
    .login{
        display: flex;
        width: 100%;
        box-sizing: border-box;
        height: 25%;
        margin: 20px 0;
        padding-left: 10px;
        font-size: 20px;
        border-radius: 10px;
        color: rgb(95, 48, 95);
        border-color: pink;
        box-shadow: 0px 0px 5px rgba(241, 143, 200, 0.932);
    }
    .btn{
        margin-left:50%;
        transform: translateX(-50%);
        border-color: pink;
        background-color: pink;
        border-radius: 8px;
        width: 100px;
        box-shadow: 0px 0px 5px rgba(241, 143, 200, 0.932);
    }
}

</style>