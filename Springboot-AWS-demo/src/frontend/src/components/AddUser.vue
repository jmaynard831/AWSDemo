<template>
<div>
<form v-on:submit.prevent="addUser">
    <label>First Name:</label><input v-model="fname" required><br>
    <label>Last Name:</label><input v-model="lname" required><br>
    <label>Email:</label><input v-model="email" required><br>
    <button>Add User</button>
</form>
</div>
    
</template>

<script>
export default {
  data(){
    return {
      fname:"",
      lname:"",
      email:""
    }
  },
  props:["getUsers"],
  methods:{
      addUser(){
          //take the info, run through API, and then blank the fields. 
          return fetch("/api/users", {method:"POST", headers: {'Content-Type': 'application/json'},
          body:JSON.stringify(
              {firstName: this.fname, lastName: this.lname, email:this.email}
              )})
          .then(res => {
                console.log("Response:", res);
                this.fname = ""
                this.lname = ""
                this.email=""
                this.getUsers()
                });
               
      }
  }
}
</script>

<style scoped>
div{
    background-color: gray;
    margin-block: 10px;
    max-width: 400px;
}
</style>