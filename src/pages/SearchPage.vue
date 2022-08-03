<template>
  <div class="mainIm" >
    <div style="position: absolute ; top:60%; left: 25%;">
    <h1 class="title">Search Page</h1>
      <div id="search_options">
        <form class="form-inline my-2 my-lg-0" ref="form" @submit.stop.prevent="handleSubmit" >
          <b-form-group
            label-for="name-input"
            invalid-feedback="Search key is required"
            :state="nameState"
          >
            <b-form-input
              id="search_input1"
              class="form-control mr-sm-2"
              type="search"
              placeholder="Search"
              aria-label="Search"
              v-model="search_input"
              :state="nameState"
              required
            ></b-form-input>
          </b-form-group>
        </form>
        <br>
          Choose Number Of Recipes To Return :
          <br>
        <b-form-select v-model="number" :options="options_n" style="width:65px" class="mt-3"></b-form-select>
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
          <div style="float:right" v-show="this.$root.store.arr_to_sort.length != 0">
            <b-dropdown id="dropdown-1" text="Sort" class="m-md-2" variant="warning" >
              <b-button class="bot" @click="SortPopularity">Popularity</b-button>
              <b-button class="bot" @click="SortTime">Time</b-button>
            </b-dropdown>
          </div>
        </div>
      </div>
      <div id="results">
        <RecipePreviewListSearch :recipes="this.$root.store.arr_to_sort"></RecipePreviewListSearch>
      </div>
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
        searchClicked: false,
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
        response: [],
        nameState: null,
        search_input: '',
      };
    },
    methods: {
      checkFormValidity() {
        const valid = this.$refs.form.checkValidity();
        this.nameState = valid;
        return valid;
      },
      onReset() {
      this.cuisine = null;
      this.number = 5;
      this.diet = null;
      this.intolerance = null;
    },

     async Search(){
        if (!this.checkFormValidity()) {
          return
        }

        try {
          this.response = await this.axios.get(
            // "https://test-for-3-2.herokuapp.com/recipes/info",
            // this.$root.store.server_domain + "/recipes/info",document.getElementById("search_input").value
            this.$root.store.server_domain + "/recipes/query/" + this.search_input,
            // document.getElementById("search_input").value,
            //  + "/" + this.number + "/" + this.cuisine + "/" + this.diet + "/" + this.intolerance + "/" + this.sort,
            {
              params: {
                  query: this.$route.params.query,                 
                  number: this.number,
                  cuisine: this.cuisine,
                  diet: this.diet,
                  intolerance: this.intolerance,
                }
              }
          );
          if (this.response.data.length == 0) {
             alert("There Are No Results For Your Search");
             return;
          }
          this.searchClicked = true;
          // console.log(this.response.data, "HERLLO");
          // console.log("response.status", this.response.status, this.response.length);
          if (this.response.status !== 200) this.$router.replace("/NotFound");
          this.response = this.response.data;
          this.$root.store.arr_to_sort = this.response;

        } catch (error) {
          console.log("error.response.status", error.response.status);
          this.$router.replace("/NotFound");
          return;
        }

      },
      SortPopularity(){
        this.response = [];
        let sorted_arr = this.$root.store.arr_to_sort;
        sorted_arr.sort(function comparePopularity(a,b) {
          return parseInt(a.popularity) - parseInt(b.popularity);
        });
        this.response = sorted_arr;
        this.$forceUpdate();
      },
      SortTime(){
        this.response = [];
        let sorted_arr = this.$root.store.arr_to_sort;
        sorted_arr.sort(function compareTime(a,b) {
          return parseInt(a.readyInMinutes) - parseInt(b.readyInMinutes);
        });
        this.response = sorted_arr;
        this.$forceUpdate();
      }
    }
}

</script>

<style>
/* #search_options{
  
} */
.bot{
  color: black;
    background-color: rgb(255, 255, 255);
    border: none;
}
.mainIm{
    background-image: url("../images/recipesImages/mainIMG.jpeg"); /* The image used */
    background-color: #cccccc; /* Used if the image is unavailable */
    height: 600px; /* You must set a specified height */
    background-position: center; /* Center the image */
    background-repeat: no-repeat; /* Do not repeat the image */
    background-size: cover; /* Resize the background image to cover the entire container */
}
</style>

