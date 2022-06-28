<template>
  <b-container>
    <div >
    <b-col>
      <b-row v-for="r in this.recipes.slice(0, this.recipes.length/3+1)" :key="r.id" >
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-row>
    </b-col>
    </div>
    <div>
    <b-col>
      <b-row v-for="r in this.recipes.slice(this.recipes.length/3+1, ((this.recipes.length/3))*2)" :key="r.id" >
        <RecipePreview class="recipePreview" :recipe="r" />
        </b-row>
    </b-col>
    </div>
    <div>
    <b-col>
      <b-row v-for="r in this.recipes.slice(((this.recipes.length/3) +1)*2, this.recipes.length)" :key="r.id" >
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-row>
    </b-col>
    </div>
  </b-container>
</template>

<script>
import RecipePreview from "../components/RecipePreview.vue";
import { floor } from "mathjs";
export default {
  name: "RecipePreviewFavorites",
  components: {
    RecipePreview,
  },
  props: {
    title: {
      type: String,
    }
  },
  data() {
    return {
      recipes: []
    };
  },
  async created() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/users/favorites");

        const recipes = response.data.recipes;
        this.recipes = [];
        this.recipes.push(...recipes);
        console.log(this.recipes.length);
      } catch (error) {
        console.log(error);
      }
    }
};
</script>

<style lang="scss" scoped>
b-container {
  min-height: 400px;
}
b-col{
    // padding: 100px;
    // margin: 100px;
}
b-row{
    // padding: 100px;
    // margin: 100px;
}
div{
    padding: 10px;
}
</style>