<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <div style="display:inline-block">
      <div style="display:inline-block; margin-left:100px">
        <RecipePreviewList title="Random Recipes" class="RandomRecipes center" />
      </div>
      <div style="display:inline-block; margin-left:300px;">
        <!-- <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</router-link> -->
        <!-- {{ !$root.store.username }} -->
        <!-- <RecipePreviewList v-if
            title="Last Viewed Recipes"
            :class="{
              RandomRecipes: true,
              blur: !$root.store.username,
              center: true
            }"
            disabled
        ></RecipePreviewList> -->
        <LoginPage v-if="!$root.store.username"></LoginPage>
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

export default {
  name: "MainPage",
  components: {
    RecipePreviewList,
    LoginPage
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
