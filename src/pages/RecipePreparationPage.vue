<template>
    <div >
        <div>
            <div class="recipe-header mt-3 mb-4" style="display: flex; justify-content: center; ">
                <h1>{{ this.title }}</h1>
                <img :src="this.image" class="center" />
            </div>
            <div style="display: flex; justify-content: center; ">
            Ingredients:
                <ul>
                <li
                    v-for="(r, index) in recipeIngredients"
                    :key="index + '_' + r.ingredientName"
                >
                    {{ r.ingredientName }} : {{ r.amount }} {{r.units}}
                </li>
                </ul>
            </div>
            <div style="display: flex; justify-content: center; ">
                <b-form-group
                label="servings : "
                label-for="servings"
                >
                <b-form-input
                    id="new_servings"
                    v-model="new_servings"
                    placeholder="amount"
                    style="width: 90px; display:inline;"
                ></b-form-input>
                <button class="btn btn-outline-warning my-2 my-sm-0" @click="multiply" style="margin-left: 10px">multiply</button>
                </b-form-group>
            </div>
            <div style="display: flex; justify-content: center; ">
                <button class="btn btn-outline-success my-2 my-sm-0" @click="Start" v-show="!flag" >Start</button>
            </div>
        </div>
        <StepsRecipe v-if="flag" :analyzedInstructions="this.analyzedInstructions" :id="this.$route.params.id"></StepsRecipe>
    </div>
</template>

<script>
import StepsRecipe from "../components/StepsRecipe";
export default {
    name: "RecipePreparationPage",
    components: { StepsRecipe },
    data(){
        return {
            recipeIngredients: [],
            analyzedInstructions: [],
            title: '',
            image: '',
            servings: '',
            new_servings: '',
            flag: false
        }
    },
    async mounted(){
        console.log(this.$route.params.id);
        const response = await this.axios.get(this.$root.store.server_domain + "/recipes/" + `${this.$route.params.id}` +"/analyzedInstructions");
        console.log(response.data); // its working
        this.recipeIngredients = response.data.recipeIngredients;
        this.analyzedInstructions = response.data.analyzedInstructions;
        this.title = response.data.title;
        this.image = response.data.image;
        this.servings = response.data.servings;

    },
    methods:{
        multiply(){
            if (this.new_servings==0){
                return;
            }
            for (let i = 0 ; i < this.recipeIngredients.length ; i++){
                this.recipeIngredients[i].amount = String(parseFloat(this.recipeIngredients[i].amount) * this.new_servings);
            }
        },
        Start(){
            this.flag = true;
        }
    }
}
</script>

<style>

</style>