<template>
<div class="neworder">
<span>
<h2> {{msg}} </h2>
</span>
<label> <b> Receipent First Name </b> </label> 
<input type="text"  v-model.lazy="neworder.recFN">
<br>
<label> <b> Receipent Last Name </b> </label> 
<input type="text" v-model.lazy="neworder.recLN">
<br>
<label> <b> Gift Card Value </b> </label> 
<input type="number" v-model.lazy="neworder.gcv">
<br>
<label> <b> Amount </b> </label> 
<input type="number" v-model.lazy="neworder.comAmt">
<br>
<label> <b> Receipent Mobile No </b> </label> 
<input type="number" v-model.lazy="neworder.recMob">
<br>
<label> <b> Address </b> </label> 
<input type="textarea" v-model.lazy="neworder.addr">
<br>
<button type="button" v-on:click="PlaceOrder()"> Place Order </button>
</div>
</template>

<script>
export default {
    name:'neworder',
    data:function(){
        return{
            msg:"Place Order Here",
            neworder:{
                "recFN":"",
                "recLN":"",
                "gcv":"",
                "comAmt":"",
                "recMob":"",
                "addr":""
            },
            error:[]
        }
    },
    methods:{
        PlaceOrder: function(){
           let valPlaceOrder = this.ValidatePO()
      if(localStorage){
          localStorage.setItem("neworder"+this.neworder.id, JSON.stringify(this.neworder))
      }
      if(valPlaceOrder){
          this.$http.post('http://localhost:3000/neworder', this.neworder)
          .then(res=>{
              console.log(res)
          },err=>{
              console.log(err)
          })
      }
    },
    ValidatePO: function(){
       console.log("Placing new Order")
       if(this.neworder.id == 0){
       this.error.push("Id must be non zero")
       return false
     }

     return true
    }

    }
}
</script>