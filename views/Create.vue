<template>
  <form class="create-wrapper" :bond = "createContent" >
       <div class="success" v-show = 'submitted'>
       <div>You have successfully submitted! Good!</div> 
      </div>
    <div class="title formItem " v-show = '! submitted' >
      <div class="formLabel">Title</div>
      <input type="text" v-model= "createContent.title">
    </div>
    <div class="sel formItem" v-show = '! submitted'>
      <div class="formLabel">Category</div>
      <select v-model= "createContent.category" class="formItem">
        <option value= "vue">Vue</option>
        <option value= "database">Database</option>
        <option value= "axios">Axios</option>
      </select>
    </div>
    <div class="context formItem" v-show = '! submitted'>
      <div class="formLabel">Content</div>
      <textarea v-model= "createContent.context">
      </textarea>

    </div>
    <div class="btn" v-show = '! submitted'>
      <button @click.prevent = "submit">Submit</button>
    </div>
 
    
  </form>
</template>

<script>
import {db} from '../utils/firebase'
import { collection,addDoc } from "firebase/firestore"
export default {
  name:'Create',
  data() {
    return {
      createContent:{ 
        title:'',
        category:'',
        context:'',
      },
      submitted:false,
      
    }
  
  },
  methods:{
    async submit(){ 
      console.log(this.createContent)
      // Add a second document with a generated ID.
    try {
      const docRef = await addDoc(collection(db, "memo"),this.createContent)
      console.log("Document written with ID: ", docRef.id);
      this.submitted = true
      setTimeout(()=>{
        this.$router.push('/home')
      },2000)
      

    } catch (e) {
      console.error("Error adding document: ", e);
      }
    }
  }

}
</script>

<style lang="less" scoped>

.create-wrapper{
  margin-top:10px;
  .sel{
    margin-top: 10px;
    text-align: left;
    select{
      margin: 5px;
      margin-left:0px;
      border-radius: 10px;
      font-size: 15px;
      border: none;
      color: rgb(209, 130, 130);
      padding:5px;
      box-shadow: 0px 0px 5px rgba(214, 49, 76, 0.5);  
    }  
  }
    .formLabel{
      margin-top: 5px;
      margin-bottom: 5px;
      text-align: left;
      font-size: 20px;
    }

    input{
      padding: 5px;
      padding-left:10px;
      width: 100%;
      box-sizing: border-box ;
      color: rgb(238, 108, 108);
      border-radius: 10px;
      border: none;
      box-shadow: 0px 0px 5px rgba(214, 49, 76, 0.5);
    }  
  }
  textarea{
    width: 100%;
    box-sizing: border-box;
    height: 500px;
    border: none;
    border-radius: 10px;
    padding: 10px;
    color: rgb(177, 102, 102);
    box-shadow: 0px 0px 5px rgba(214, 49, 76, 0.5);
    }
  .btn{
    float: right;
    button{
      margin-left: 20px;
      width: 100px;
      border-radius: 10px;
      border:none;
      background-color:rgb(240, 238, 238);
      color: rgb(238, 108, 108);
    }
  }
  .success{
    width:500px;
    height:500px;
    position:absolute;
    left:30%;
    background-color:pink;
    text-align: center;
    box-shadow: 0px 0px 5px rgba(214, 49, 76, 0.5);
    border-radius: 10px;
    div{
      margin: 30% auto;
      font-size: 40px;
      color: rgb(177, 102, 102);
    }

  }
  .trans{
    opacity: 30%;
  }
  



</style>
