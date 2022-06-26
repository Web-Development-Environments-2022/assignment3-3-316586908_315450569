<template>

  <div class="container">
    <h1 class="title">Search Page</h1>
      <div id="search_options">
        <form class="form-inline my-2 my-lg-0">
          <input id="search_input" class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
        </form>
        <br>
          Choose Number Of Recipes To Return :
          <br>
        <b-form-select v-model="number" :options="options_n" style="width:65px" class="mt-3"></b-form-select>
        <!-- <div class="mt-3">Selected: <strong>{{ selected }}</strong></div> -->
        <br>
        <div >
          <div style="display:inline-block; padding:5px;">
            <h5>cuisine : </h5>
          <b-form-select v-model="cuisine" :options="options_c" size="sm" class="mt-3" style="width:150px;"></b-form-select>
          </div>
          
          <div style="display:inline-block; padding:5px;">
            <h5>diet : </h5>
          <b-form-select v-model="diet" :options="options_d" size="sm" class="mt-3" style="width:150px"></b-form-select>
          </div>
          
          <div style="display:inline-block; padding:5px;">
            <h5>intolerance : </h5>
          <b-form-select v-model="intolerance" :options="options_i" size="sm" class="mt-3" style="width:150px"></b-form-select>
          </div>
        </div>
        <br>
        <div>
          <div style="display:inline-block; padding:20px">
            <button class="btn btn-outline-success my-2 my-sm-0" type="submit" @click="Search">Search</button>
          </div>
          <div style="display:inline-block"> 
            <b-button type="reset" variant="danger" @click="onReset">Reset</b-button>
          </div>
        </div>
      </div>
      <div id="results">
        <RecipePreviewListSearch :recipes="this.response.data"></RecipePreviewListSearch>
      </div>
  </div>
  
</template>

<script>
import RecipePreviewListSearch from "../components/RecipePreviewListSearch";
export default {
  name: "SearchPage",
  components: { RecipePreviewListSearch },
  data() {
      return {
        number: 5,
        options_n: [
          { value: 5, text: '5' },
          { value: 10, text: '10' },
          { value: 15, text: '15'}
        ],
        cuisine: null,
        options_c:[
          "African","American","British","Cajun","Caribbean","Chinese","Eastern European","European","French","German","Greek",
          "Indian","Irish","Italian","Japanese","Jewish","Korean","Latin American","Mediterranean","Mexican","Middle Eastern",
          "Nordic","Southern","Spanish","Thai","Vietnamese"
        ],
        diet: null,
        options_d:[
          "gluten free", "ketogenic", "vegetarian", "lacto-vegetarian", "ovo-vegetarian", "vegan", "pescetarian", "paleo",
          "primal", "low fodmap", "whole30"
        ],
        intolerance: null,
        options_i:[
          "dairy", "egg", "gluten", "grain", "peanut", "seafood", "sesame", "shellfish", "soy", "sulfite", "tree nut" , "wheat"
        ],
        sort: null,

        response: []

      }
    },
    methods: {
      onReset() {
      this.cuisine = null;
      this.number = 5;
      this.diet = null;
      this.intolerance = null;
    },
     async Search(){
          // let response;
          // response = this.$route.params.response;

        try {
          this.response = await this.axios.get(
            // "https://test-for-3-2.herokuapp.com/recipes/info",
            // this.$root.store.server_domain + "/recipes/info",document.getElementById("search_input").value
            this.$root.store.server_domain + "/recipes/query" + "/" + document.getElementById("search_input").value,
            //  + "/" + this.number + "/" + this.cuisine + "/" + this.diet + "/" + this.intolerance + "/" + this.sort,
            {
              params: {
                  query: this.$route.params.query,                 
                  number: this.number,
                  cuisine: this.cuisine,
                  diet: this.diet,
                  intolerance: this.intolerance,
                  sort: this.sort,
                }
              }
          );
          // console.log(this.response.data, "HERLLO");
          // console.log("response.status", this.response.status, this.response.length);
          if (this.response.status !== 200) this.$router.replace("/NotFound");
        } catch (error) {
          console.log("error.response.status", error.response.status);
          this.$router.replace("/NotFound");
          return;
        }

      }
    }
    
}

</script>

<style>
/* #search_options{
  
} */
</style>

