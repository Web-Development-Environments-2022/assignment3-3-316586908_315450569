<template>
  <div class="imgDiv" >
    <div style="position: relative; top: 400px;">

      <div style="display:inline">
        <div style="display:inline; float:left; margin-right:50px;">
          <RecipePreviewList title="Random Recipes" class="RandomRecipes center" />
          <b-button variant="dark" @click="Refresh" style="position: relative;  left: 400px; bottom:100px">Refresh</b-button>
        </div>
        <div style="display:sticky; float:right; margin-left:5px; margin-top:5px ;">
          <LoginPage v-if="!$root.store.username" style=" position: absolute;  left: 60%;"></LoginPage>
          <RecipePreviewListLoggedIn v-else title="Last Watched Recipes"></RecipePreviewListLoggedIn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import LoginPage from "../pages/LoginPage";
import RecipePreviewListLoggedIn from "../components/RecipePreviewListLoggedIn";

export default {
  name: "MainPage",
  components: {
    RecipePreviewList,
    LoginPage,
    RecipePreviewListLoggedIn
  },
  methods: {
    Refresh(){
      // RecipePreviewList.mounted();
      RecipePreviewList.methods.updateRecipes();
      // this.$root.$emit('RecipePreviewList');
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
