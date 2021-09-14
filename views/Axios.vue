<template>
  <div class="axios">
    <div class="content">  
      <ul>
        <li v-for= "cl in contentList" :key = 'cl.id'>
          <router-link :to="'/home/singleblog/'+cl.id">
          <h3>{{cl.data().title}}</h3>
          <h4>{{cl.data().context}}</h4>
          </router-link>
        </li>
      </ul>
    </div>    
  </div>
</template>

<script>
import { getDocs,collection } from '@firebase/firestore';
import {db} from '../utils/firebase'
export default {
name:'Databse',
data() {
    return {
      contentList:[],
    } 
  },
  methods:{
    async setContent(){
      const querySnapshot = await getDocs(collection(db, "memo"));
       querySnapshot.forEach((doc) => {
         if(doc.data().category == 'axios'){
           this.contentList.push(doc)
         }
     // console.log(`${doc.id} => ${doc.data().category}`);
       })
    }
  },
  mounted() {
    this.setContent()  
  }

}
</script>

<style lang ='less' scoped>
ul{
  padding-top:20px;
  li{
  margin-bottom: 10px;
  height: 150px;
  list-style: none;
  background-color:rgb(240, 238, 238);
  border: none;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0px 0px 5px rgba(214, 49, 76, 0.5);
  h3{
    color: rgb(238, 108, 108);
  }
  h4{
    color: rgb(218, 163, 163);
  }
  }
}


</style>