<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <div style="display:inline">
      <div style="display:inline; float:left; margin-right:50px;">
        <RecipePreviewList title="Random Recipes" class="RandomRecipes center" />
      </div>
      <div style="display:sticky; float: right; margin-left:5px; margin-top:5px">
        <LoginPage v-if="$root.store.username"></LoginPage>
        <RecipePreviewListLoggedIn v-else title="Last Watched Recipes"></RecipePreviewListLoggedIn>
      </div>
    </div>
    
    <!-- <div
      style="position: absolute;top: 70%;left: 50%;transform: translate(-50%, -50%);"
    >
      Centeredasdasdad
    </div>-->
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
</style>
