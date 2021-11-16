<template>
  <div>
    
  <div v-for="(user,i) in message" :key="i" class="tile">
    <div>
    <h1>{{user.firstName}} {{user.lastName}}</h1>
    <ul><li>{{user.email}}</li></ul>
    </div>
    <button @click="deleteUser(user.id)">Delete User</button><br>
    <button>Update User</button></div>
  
  <!-- just add a panel and v-if its visibility  -->

  
  </div>
  
  <AddUser v-bind:getUsers="getUsers"/>
</template>

<script>

import AddUser from '../components/AddUser.vue'
export default {
  data(){
    return {
      message:{}
    }
  },
  components: {
    AddUser
  },
  methods:{
    deleteUser(userId){
      console.log(userId)
       return fetch("/api/users/"+userId, {method:"DELETE", headers: {'Content-Type': 'application/json'}})
        .then((res)=>{
          console.log(res)
          this.getUsers()
        })
    },
    getUsers(){
      fetch("/api/users")
        .then((response)=>response.json())
        .then((data)=>{
           this.message = data;
          })
    }
  },
  mounted(){
    this.getUsers()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tile{
  background-color: #F2AF29;
}
.tile{
  max-width: 400px;
}
button{
  margin-block: 5px;
}

</style>
