<template>
  <div>
    <b-container>
        <br>
        <button v-if="this.Meal.length != 0" class="btn btn-warning" @click="removeAll" style="float: right">Remove All</button>
        <b-row>
        <b-col v-for="r in this.Meal.slice(0,3)" :key="r.recipe.id">
            <div style="display:inline-block;">
                <div style="margin-left: 42px">
                    <RecipePreview class="recipePreview" :recipe="r.recipe"></RecipePreview>
                </div>
                <div style="display: flex ;  ">
                    <div style="display:inline;">
                        <button class="btn btn-secondary" @click="moveLeft(r.recipe.id)">
                            <i class="bi bi-arrow-left"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-left" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M15 8a.5.5 0 0 0-.5-.5H2.707l3.147-3.146a.5.5 0 1 0-.708-.708l-4 4a.5.5 0 0 0 0 .708l4 4a.5.5 0 0 0 .708-.708L2.707 8.5H14.5A.5.5 0 0 0 15 8z"/>
                            </svg>
                        </button>
                    </div>
                    <div style="display:inline; ">
                        <label v-if="r.recipe.curr_step == 0" style="display:flex;margin-right: 85px ;margin-left: 75px; font-weight: bold">{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</label>
                        <b-progress v-else :max="r.recipe.total_steps" :variant="'info'" height="2.4rem" style="width:192px" show-value striped show-progress>
                            <b-progress-bar :value="r.recipe.curr_step" :max="r.recipe.total_steps" show-value striped show-progress>
                                <span><strong>{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</strong></span>
                            </b-progress-bar>
                        </b-progress>
                    </div>
                    <div style="display:inline">
                        <button class="btn btn-secondary" @click="moveRight(r.recipe.id)">
                            <i class="bi bi-arrow-right"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-right" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
                            </svg>
                        </button>
                    </div>
                </div>
                <br>
                <div style="margin-left: 80px">
                    <button class="btn btn-danger" @click="remove(r.recipe.id)">Remove</button>
                </div>
            </div>
        </b-col>
        </b-row>
        <br>
        <b-row>
        <b-col v-for="r in this.Meal.slice(3,6)" :key="r.recipe.id">
            <div style="display:inline-block;">
                <div style="margin-left: 42px">
                    <RecipePreview class="recipePreview" :recipe="r.recipe"></RecipePreview>
                </div>
                <div style="display: flex ;  ">
                    <div style="display:inline;">
                        <button class="btn btn-secondary" @click="moveLeft(r.recipe.id)">
                            <i class="bi bi-arrow-left"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-left" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M15 8a.5.5 0 0 0-.5-.5H2.707l3.147-3.146a.5.5 0 1 0-.708-.708l-4 4a.5.5 0 0 0 0 .708l4 4a.5.5 0 0 0 .708-.708L2.707 8.5H14.5A.5.5 0 0 0 15 8z"/>
                            </svg>
                        </button>
                    </div>
                    <div style="display:inline; ">
                        <label v-if="r.recipe.curr_step == 0" style="display:flex;margin-right: 85px ;margin-left: 75px; font-weight: bold">{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</label>
                        <b-progress v-else :max="r.recipe.total_steps" :variant="'info'" height="2.4rem" style="width:192px" show-value striped show-progress>
                            <b-progress-bar :value="r.recipe.curr_step" :max="r.recipe.total_steps" show-value striped show-progress>
                                <span><strong>{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</strong></span>
                            </b-progress-bar>
                        </b-progress>
                    </div>
                    <div style="display:inline">
                        <button class="btn btn-secondary" @click="moveRight(r.recipe.id)">
                            <i class="bi bi-arrow-right"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-right" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
                            </svg>
                        </button>
                    </div>
                </div>
                <br>
                <div style="margin-left: 80px">
                    <button class="btn btn-danger" @click="remove(r.recipe.id)">Remove</button>
                </div>
            </div>
        </b-col>
        </b-row>
        <br>
        <b-row>
        <b-col v-for="r in this.Meal.slice(6,9)" :key="r.recipe.id">
            <div style="display:inline-block;">
                <div style="margin-left: 42px">
                    <RecipePreview class="recipePreview" :recipe="r.recipe"></RecipePreview>
                </div>
                <div style="display: flex ;  ">
                    <div style="display:inline;">
                        <button class="btn btn-secondary" @click="moveLeft(r.recipe.id)">
                            <i class="bi bi-arrow-left"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-left" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M15 8a.5.5 0 0 0-.5-.5H2.707l3.147-3.146a.5.5 0 1 0-.708-.708l-4 4a.5.5 0 0 0 0 .708l4 4a.5.5 0 0 0 .708-.708L2.707 8.5H14.5A.5.5 0 0 0 15 8z"/>
                            </svg>
                        </button>
                    </div>
                    <div style="display:inline; ">
                        <label v-if="r.recipe.curr_step == 0" style="display:flex;margin-right: 85px ;margin-left: 75px; font-weight: bold">{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</label>
                        <b-progress v-else :max="r.recipe.total_steps" :variant="'info'" height="2.4rem" style="width:192px" show-value striped show-progress>
                            <b-progress-bar :value="r.recipe.curr_step" :max="r.recipe.total_steps" show-value striped show-progress>
                                <span><strong>{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</strong></span>
                            </b-progress-bar>
                        </b-progress>
                    </div>
                    <div style="display:inline">
                        <button class="btn btn-secondary" @click="moveRight(r.recipe.id)">
                            <i class="bi bi-arrow-right"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-right" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
                            </svg>
                        </button>
                    </div>
                </div>
                <br>
                <div style="margin-left: 80px">
                    <button class="btn btn-danger" @click="remove(r.recipe.id)">Remove</button>
                </div>
            </div>
        </b-col>
        </b-row>
        <br>
        <b-row>
        <b-col v-for="r in this.Meal.slice(9,12)" :key="r.recipe.id">
            <div style="display:inline-block;">
                <div style="margin-left: 42px">
                    <RecipePreview class="recipePreview" :recipe="r.recipe"></RecipePreview>
                </div>
                <div style="display: flex ;  ">
                    <div style="display:inline;">
                        <button class="btn btn-secondary" @click="moveLeft(r.recipe.id)">
                            <i class="bi bi-arrow-left"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-left" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M15 8a.5.5 0 0 0-.5-.5H2.707l3.147-3.146a.5.5 0 1 0-.708-.708l-4 4a.5.5 0 0 0 0 .708l4 4a.5.5 0 0 0 .708-.708L2.707 8.5H14.5A.5.5 0 0 0 15 8z"/>
                            </svg>
                        </button>
                    </div>
                    <div style="display:inline; ">
                        <label v-if="r.recipe.curr_step == 0" style="display:flex;margin-right: 85px ;margin-left: 75px; font-weight: bold">{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</label>
                        <b-progress v-else :max="r.recipe.total_steps" :variant="'info'" height="2.4rem" style="width:192px" show-value striped show-progress>
                            <b-progress-bar :value="r.recipe.curr_step" :max="r.recipe.total_steps" show-value striped show-progress>
                                <span><strong>{{ r.recipe.curr_step }} / {{ r.recipe.total_steps }}</strong></span>
                            </b-progress-bar>
                        </b-progress>
                    </div>
                    <div style="display:inline">
                        <button class="btn btn-secondary" @click="moveRight(r.recipe.id)">
                            <i class="bi bi-arrow-right"></i>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-right" viewBox="0 0 16 16">
                                <path fill-rule="evenodd" d="M1 8a.5.5 0 0 1 .5-.5h11.793l-3.147-3.146a.5.5 0 0 1 .708-.708l4 4a.5.5 0 0 1 0 .708l-4 4a.5.5 0 0 1-.708-.708L13.293 8.5H1.5A.5.5 0 0 1 1 8z"/>
                            </svg>
                        </button>
                    </div>
                </div>
                <br>
                <div style="margin-left: 80px">
                    <button class="btn btn-danger" @click="remove(r.recipe.id)">Remove</button>
                </div>
            </div>
        </b-col>
        </b-row>
    </b-container>
  </div>
</template>

<script>
import RecipePreview from "../components/RecipePreview"
export default {
    components: { RecipePreview },
    data(){
        return {
            Meal : this.$root.store.Meal
        }
    },
    methods: {
        remove(id){
            let found = this.Meal.findIndex(element => {
                return element.recipe.id == id;
            });
            this.Meal.splice(found,1);

            found = this.$root.store.recipesAtMeal.findIndex(element => {
                return element.recipe.id == id;
            });
            this.$root.store.recipesAtMeal.splice(found,1);
        },
        moveRight(id){
            let found = this.Meal.findIndex(element => {
                return element.recipe.id == id;
            });
            if (found == this.Meal.length - 1)
                return;
            else{
                let tmp = this.Meal[found + 1];
                this.Meal[found + 1] = this.Meal[found];
                this.Meal[found] = tmp;
            }
            this.$forceUpdate();
        },
        moveLeft(id){
            let found = this.Meal.findIndex(element => {
                return element.recipe.id == id;
            });
            if (found == 0)
                return;
            else{
                let tmp = this.Meal[found - 1];
                this.Meal[found - 1] = this.Meal[found];
                this.Meal[found] = tmp;
            }
            this.$forceUpdate();
        },
        removeAll(){
            this.$root.store.Meal = [];
            this.$root.store.recipesAtMeal = [];
            this.Meal = [];
            this.$forceUpdate();
        }
  },
}
</script>

<style>

</style>