<template>
  <div class="imgDiv" >
    <div style="position: relative; top: 400px;">

      <div style="display:inline">
        <div style="display:inline; float:left; margin-right:50px;">
          <RecipePreviewList title="Explore This Recipes" class="RandomRecipes center" ref="recipepreview"/>
          <b-button variant="dark" @click="Refresh" style="position: relative;  left: 400px; bottom:0px">Refresh</b-button>
          <br>
          <br>
          <br>
        </div>
        <div style="display:sticky; float:right; margin-left:5px; margin-top:5px ;">
          <LoginComponent v-if="!$root.store.username" style=" position: absolute;  left: 70%; top: 100px;"></LoginComponent>
          <RecipePreviewListLoggedIn v-else title="Last Watched Recipes" style="margin-right: 200px"></RecipePreviewListLoggedIn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import LoginComponent from "../components/LoginComponent";
import RecipePreviewListLoggedIn from "../components/RecipePreviewListLoggedIn";

export default {
  name: "MainPage",
  components: {
    RecipePreviewList,
    LoginComponent,
    RecipePreviewListLoggedIn
  },
  methods: {
    async Refresh(){
      this.$refs.recipepreview.updateRecipes();
      console.log("CLICKED");
    }
  }
};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  margin: 10px 0 10px;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
.imgMain{
  left: 0;
  max-width: 100%;
  max-height: 100%;

}

.imgDiv{
   background-image: url("../images/recipesImages/avi2.jpeg"); /* The image used */
    background-color: #cccccc; /* Used if the image is unavailable */
    height: 400px; /* You must set a specified height */
    background-position: center; /* Center the image */
    background-repeat: no-repeat; /* Do not repeat the image */
    background-size: cover; /* Resize the background image to cover the entire container */
}

</style>
