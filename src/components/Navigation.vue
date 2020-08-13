<template>
    <div>
        <ul>
            <li>
                <router-link to="/" exact>Home </router-link>
                <br>
                <router-link to="/register" exact>Register</router-link>
              
                <router-link to="/login" exact>Log In</router-link>
              
                 <router-link to="/admin" exact> Admin</router-link>
                 
                
        
            </li>
        </ul>
    </div>
</template>

<script>
export default {
}
</script>

<style scoped>

.router-link-active{
    background-color: lightgrey;
    color: red;
}

li{
    display: inline-block;
    margin: 10px;
    padding: 10px;

}

ul{
    list-style-type: none;

}


</style>