<template>
  <b-container>
    <div >
    <b-row>
      <b-col v-for="r in this.recipes.slice(0, 5)" :key="r.id" >
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
    </div>
    <div>
    <b-row>
      <b-col v-for="r in this.recipes.slice(5, 10)" :key="r.id" >
        <RecipePreview class="recipePreview" :recipe="r" />
        </b-col>
    </b-row>
    </div>
    <div>
    <b-row>
      <b-col v-for="r in this.recipes.slice(10, 15)" :key="r.id" >
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-col>
    </b-row>
    </div>
  </b-container>
</template>

<script>
import RecipePreview from "../components/RecipePreview";
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
