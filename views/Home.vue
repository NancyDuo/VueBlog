<template>
  <div class="home">
    <div class="content">  
      <ul>
        <li v-for= "cl in contentList" :key = 'cl.id'>
          <router-link :to="'/home/singleblog/'+cl.id">
          <h3>{{cl.data().title}}</h3>
          <h4>{{cl.data().emotion}}</h4>
          </router-link>
          <!-- <h5>{{cl.data().context}}</h5> -->
        </li>
      </ul>
    </div>    
  </div>
</template>

<script>
import { getDocs,collection,doc } from '@firebase/firestore';
import {db} from '../utils/firebase'

export default {
  name: 'Home',
  data() {
    return {
      contentList:[],
    } 
  },
  methods:{
    async setContent(){
      const querySnapshot = await getDocs(collection(db, "memo"));
      this.contentList = querySnapshot.docs
      // console.log(this.contentList[0])
      // querySnapshot.forEach((doc) => {
      //   this.contentList = doc.data() 
        // this.contentList.id = doc.id,
        // this.contentList.name = doc.data().name
        // console.log(`${doc.id} => ${doc.data().name}`);
      // })
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