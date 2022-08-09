<template>
  <div>
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <!-- <a class="navbar-brand" href="#">Ido&Tal Recipes</a> -->
        <img src="../images/recipesImages/logo.png" class="logo">
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav >
          <b-navbar-nav>
            <router-link id="routLink" :to="{ name: 'main' }" class="nav-link" style="margin-right: 10px;margin-left: 20px; font-size: 17px;">Home</router-link>
            <router-link id="routLink" :to="{ name: 'search' }" class="nav-link" style="margin-right: 10px;margin-left: 20px; font-size: 17px;">Search </router-link>
            <router-link id="routLink" :to="{ name: 'about' }" class="nav-link" style="margin-right: 10px;margin-left: 20px; font-size: 17px;">About </router-link>
          </b-navbar-nav>
        </b-collapse>
    <div id="guest_logged">
      <span v-if="!$root.store.username">
        <h5 style="display:inline; font-family:Cursive; font-size: 15px; text-transform: uppercase; color: lightcoral;margin-right: 15px; font-size: 17px; ">Hello Guest </h5>
        <div style="display:inline-block">
        <b-collapse id="nav-collapse" is-nav >
          <b-navbar-nav>
            <router-link id="routLink" :to="{ name: 'register' }" class="nav-link" style="display:inline-block;margin-right: 15px; font-size: 17px;">Register </router-link>
            <router-link id="routLink" :to="{ name: 'login' }" class="nav-link" style="display:inline-block;margin-right: 15px; font-size: 17px;">Login </router-link>
            </b-navbar-nav>
        </b-collapse>
        </div>
      </span>
      <span v-else style="display:inline; ">
        <h5 style="display:inline; font-family:Cursive; font-size: 15px; text-transform: uppercase; color: lightcoral;margin-right: 15px; font-size: 17px;">{{ $root.store.username }} </h5>
        <h5 style="display:inline; font-family:Cursive; font-size: 15px; text-transform: uppercase; color: white;margin-right: 15px; font-size: 17px;">Meal Consist <strong style="color:lightcoral">{{this.$root.store.Meal.length}}</strong> Recipes</h5>
        <div style="display:inline;" >
          <div style="display:inline;" >
            <b-dropdown id="dropdown-1" text="Personal" variant="outline-light" style="margin-right: 15px; font-size: 17px;">
              <router-link id="routLink" :to="{ name: 'favorites' }" class="nav-link" >My Favorites</router-link>
              <router-link id="routLink" :to="{ name: 'myRecipes' }" class="nav-link">My Recipes</router-link>
              <router-link id="routLink" :to="{ name: 'familyRecipes' }" class="nav-link">Family Recipes</router-link>
              <router-link id="routLink" :to="{ name: 'MyMeal' }" class="nav-link">My Meal</router-link>

            </b-dropdown>
          </div>
            <div style="display:inline-block">
                <!-- <router-link id="routLink" :to="{ name: 'createRecipe' }" class="nav-link" style="display:inline-block">Create Recipe</router-link> -->
                <b-button variant="outline-light" v-b-modal.modal-prevent-closing style="margin-right: 15px; font-size: 17px;">Create Recipe</b-button>
                <CreateRecipeModal> </CreateRecipeModal>
            </div>
            <div style="display:inline">
                <button id="logout_button" @click="Logout" class="btn btn-outline-success my-2 my-sm-0" style="margin-right: 15px; font-size: 17px;" >Logout </button>
            </div>
            
        </div>
      </span>
      </div>
    
    </nav>
    </div>
</template>

<script> 
import CreateRecipeModal from "./CreateRecipeModal";
export default {
    name: "Navbar",
    components: { CreateRecipeModal },
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
.logo{
  width: 150px;
  height: 67px;
}

</style>