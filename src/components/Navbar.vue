<template>
  <div>
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a class="navbar-brand" href="#">Ido&Tal Recipes</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <router-link id="routLink" :to="{ name: 'main' }" class="nav-link">Main</router-link>
      <router-link id="routLink" :to="{ name: 'search' }" class="nav-link">Search </router-link>
      <router-link id="routLink" :to="{ name: 'about' }" class="nav-link">About </router-link>
    </div>
    <div id="guest_logged">
      <span v-if="!$root.store.username">
        Hello Guest:
        <div style="display:inline-block">
            <router-link id="routLink" :to="{ name: 'register' }" class="nav-link" style="display:inline-block">Register </router-link>
            <router-link id="routLink" :to="{ name: 'login' }" class="nav-link" style="display:inline-block">Login </router-link>
        </div>
      </span>
      <span v-else style="display:inline; ">
        <h5 style="display:inline; font-family:Cursive; text-transform: uppercase; color: blue">{{ $root.store.username }} : </h5>
         
        <div style="display:inline; ">
            <div class="dropdown" style="display:inline;">
              <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                Personal
              </button>
              <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                <router-link class="dropdown-item" href="#">Action</router-link>
                <router-link class="dropdown-item" href="#">Another action</router-link>
                <router-link class="dropdown-item" href="#">Something else here</router-link>
              </div>
            </div>
            <div style="display:inline-block">
                <router-link id="routLink" :to="{ name: 'login' }" class="nav-link" style="display:inline-block">Create Recipe </router-link>
            </div>
            <div style="display:inline">
                <button id="logout_button" @click="Logout" class="btn btn-outline-success my-2 my-sm-0" >Logout </button>
            </div>
            
        </div>
      </span>
      </div>
    
    </nav>
    </div>
</template>

<script> 

export default {
    name: "Navbar",
    methods: {
      Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
     }
    }
};

</script>

<style>
#guest_logged{
  display: inline;
  float: right;
}
#logout_button{
  color:red;
  border-color:red
}
#logout_button:hover{
  background-color: red;
  color: white;
}
</style>