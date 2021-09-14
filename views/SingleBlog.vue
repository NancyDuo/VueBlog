<template>
  <div class="wrapper">
      <h1>{{contentList.title}}</h1>
      <article>
         {{contentList.context}} 
      </article>      
  </div>
</template>

<script>
import {doc,getDoc} from '@firebase/firestore';
import {db} from '../utils/firebase'
export default {
    name:'SingleBlog',
    data() {
        return {
            id:this.$route.params.id,
            contentList:{
                title:'',
                context:""
            }
        }
    },
    methods:{
        async setContent(){        
        const querySnapshot = await getDoc(doc(db, "memo", this.id))
        this.contentList = querySnapshot.data()
        }
    },
    mounted() {
        this.setContent()
    },
}
</script>

<style scoped>
.wrapper{
    margin-top:20px;
    background-color:rgb(240, 238, 238);
    border: none;
    border-radius: 10px;
    padding: 10px;
    height: 800px;
    box-shadow: 0px 0px 5px rgba(214, 49, 76, 0.5);
}
h1{
    color:rgb(238, 108, 108);
    margin-top:10px;
}
article{
     color: rgb(211, 107, 107);
     
}

</style>