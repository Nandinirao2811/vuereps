<template>
<div class="login">
<span>
<h1> {{msg}} </h1>
</span>
<form>
<label> <b> User Name </b> </label> 
<br>
<input type="text" v-model.lazy="login.userName" required >
 <br>
 <label> <b> Password </b> </label> 
<br>
<input type="text" v-model.lazy="login.password" required >
<br>
<button type="button"  v-on:click="LoginBloom()">Log-In</button>
      </form>
</div>
</template>
<script>
export default {
  name: 'Login',
  data: function(){
    return {
          msg:"Login Here for Bloom Gift Cards",
       //   id: this.$route.params.myid,
          login:{
             "userName":"",
             "password": ""
             
          },
          error:[]
      }
  },
  methods:{
 LoginBloom(){
    let validLoginBloom = this.ValidateLogin()
          if(localStorage){
            localStorage.setItem("login"+this.login.id, JSON.stringify(this.login))
        }
        if(validLoginBloom){
             
   this.$http.get("http://localhost:3000/login")
   .then(res=>{
    //   console.log(this.userName, this.password)
      console.log(res)
       this.$router.push({path:'/userprofile'})
   },err=>{
     console.log(err)
   })
  }
   
 },
 ValidateLogin: function(){
   console.log("Validating User Credentials... Please Wait...")
   if(this.login.id >= 1){
     console.log("id log checking")
       this.error.push("Id must be non zero")
       return false
     }
    
        if(this.login.userName == "" && this.login.password == ""){
      //   console.log(this.login.userName, this.login.password)
       this.error.push("wrong")
       console.log("wrong credentials")
       return false
     }else{
       console.log("Welcome User ")
        console.log(this.login.userName, this.login.password)
     
     }
     
     
     return true
 }
  }


}
</script>