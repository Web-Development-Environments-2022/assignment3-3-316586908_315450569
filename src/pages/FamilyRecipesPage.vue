<template>
  <div dir="rtl">
    <div id="firstres" >
        <center>
        <div v-for="recipe in this.recipes" :key="recipe.id">
            <br>
            <div class="recipe-header mt-3 mb-4" style="font-style: italic; font-weight: bold; font-size: 20px" >
                <h1 >{{ recipe.title }}</h1>
                <br>
                <br>
                <br>
                <img :src="recipe.image" class="center" />
            </div>
            <div style="font-style: italic; font-weight: bold; font-size: 20px" >
                <br>
                <br>
                <br >
                {{recipe.instructions[0]}}
                <br >
                {{recipe.instructions[1]}}
            </div>
            <br>
            <div class="recipe-body" style="font-style: italic; font-weight: bold; font-size: 20px" >
                <div class="wrapper" >
                    <div class="wrapped" >
                        <div >
                            <div > זמן הכנה : 
                                {{ recipe.readyInMinutes }}
                                דקות
                                </div>
                            <div >טבעוני : 
                                <svg  v-if="recipe.vegan" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check" viewBox="0 0 16 16">
                                <path  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"/>
                                </svg>
                                <svg  v-else xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                                <path  d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                                </svg>
                            </div>
                            <div >צמחוני :
                                <svg  v-if="recipe.vegetarian" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check" viewBox="0 0 16 16">
                                <path  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"/>
                                </svg>
                                <svg  v-else xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                                <path  d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                                </svg>
                            </div>
                            <div >ללא גלוטן :
                                <svg v-if="recipe.glutenFree" xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check" viewBox="0 0 16 16">
                                <path  d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"/>
                                </svg>
                                <svg  v-else xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                                <path  d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                                </svg>
                            </div>
                            <div >מספר מנות :
                                {{recipe.servings}}
                            </div>
                        
                            <br>
                            <div >
                                <h3>
                                מצרכים :
                                </h3>
                                <li
                                    v-for="(r, index) in recipe.ingredients"
                                    :key="index + '_' + r.ingredientName"
                                
                                >
                                    {{ r.ingredientName }} : {{ r.amount }} {{r.units}}
                                </li>
                                
                            </div>
                        </div>
                    </div>
                    <br>
                    <div >הוראות הכנה :
                        <p >{{recipe.instructions[2]}}</p>
                    </div>
                </div>
            </div>
        </div>  
        </center>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            recipes : []
        };
    },
    async mounted(){
        try{
            const response = await this.axios.get(this.$root.store.server_domain + "/users/familyRecipes");
            const recipes = response.data.recipes;
            this.recipes = [];
            this.recipes.push(...recipes);
            this.splitInstructions();
        }
        catch (error){
            console.log(error);
        }
    },
    methods: {
        splitInstructions(){
            for (let i = 0; i < this.recipes.length; i++){
                this.recipes[i].instructions = this.recipes[i].instructions.split("|");
            }
        }
    }
}
</script>

<style>

</style>