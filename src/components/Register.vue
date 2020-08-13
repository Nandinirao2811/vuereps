<template>
<div class="Register">
<span>
<h1> {{msg}} </h1>
</span>
<form>
<label> <b> User Name </b> </label> 
<br>
<input type="text" v-model.lazy="reg.userName" required>
<br>
<label> <b>Email </b> </label>
<br>
<input type="text" v-model.lazy="reg.email" required>
<br>
<label> <b>Password </b> </label> <br>
<input type="text" v-model.lazy="reg.password" required> 
<br>
<label><b> Confirm  Password </b> </label> <br>
<input type="text" v-model.lazy="reg.confirmPassword" required>
<br>
          <button type="button"  v-on:click="RegisterBloom()">Register/SignUp</button>

</form>
</div>
</template>
<script>
export default {
  name: 'Register',
  data: function(){
    return {
          msg:"Register Here for Bloom Gift Cards",
          reg:{
             "userName":"",
             "email": "",
             "password": "",
             "confirmPassword":""
          },
          error:[]
      }
  },
  methods:{
    RegisterBloom: function(){
      let validregisterBloom = this.ValidateRegister()
      if(localStorage){
          localStorage.setItem("reg"+this.reg.id, JSON.stringify(this.reg))
      }
      if(validregisterBloom){
              this.$http.post('http://localhost:3000/register', this.reg)
                .then(res=>{
                  console.log(res)
                  this.$router.push({path:'/login'})
                }, err=>{
                  console.log(err)
                })
          }
    },
     ValidateRegister: function(){
     console.log("Validating....");
     if(this.reg.id == 0){
       this.error.push("Id must be non zero")
       return false
     }
     if(this.reg.userName === ""){
       this.error.push("Username must be provided")
       return false
     }
     if(this.reg.email === ""){
       this.error.push("Email must be provided")
       return false
     }
     
     return true
   }

  }
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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