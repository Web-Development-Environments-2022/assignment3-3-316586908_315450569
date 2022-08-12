<template>
  <div>
    <center>
        <div>
            <h4 style="color: red">Component {{stage + 1}} {{analyzedInstructions[stage].name}}</h4>
            <h4 style="color: green">step {{parseInt(analyzedInstructions[stage].steps[step].number) + 1}}</h4>
            <h5 v-show="analyzedInstructions[stage].steps[step].equipment.length != 0">Equipments : </h5>
            <li v-for="eq in analyzedInstructions[stage].steps[step].equipment" :key="eq.name">
                {{ eq.name }} 
                <p v-if="analyzedInstructions[stage].steps[step].equipment.hasOwnProperty('temperature')"> {{ eq.tmp.number }} {{ eq.tmp.unit }} </p>
            </li>
            <h5 v-show="analyzedInstructions[stage].steps[step].ingredients.length != 0">Ingredients : </h5> 
            <li v-for="ing in analyzedInstructions[stage].steps[step].ingredients" :key="ing.name">
                {{ing.name}} 
                <img :src="ing.image">
            </li>
            <h5>Instructions : </h5>
            <p>{{analyzedInstructions[stage].steps[step].step}}</p>
            <p v-if="analyzedInstructions[stage].steps[step].hasOwnProperty('length') && analyzedInstructions[stage].steps[step].length.number != ''">
                {{analyzedInstructions[stage].steps[step].length.number}} {{analyzedInstructions[stage].steps[step].length.unit}}
            </p>
        </div>
    </center>
    <div style="display: flex; justify-content: center;">
        <div style=" display: inline-block; margin-right: 300px">
            <button class="btn btn-outline-success my-2 my-sm-0" @click="prev">PREV</button>
        </div>
        {{curr_step}} / {{ total_steps }}
        <div style=" display: inline-block;margin-left: 300px">
            <button class="btn btn-outline-success my-2 my-sm-0"  @click="next">NEXT</button>
        </div>
    </div>
    <br>
  </div>
</template>

<script>
export default {
    data(){
        return{
            stage: 0,
            step: 0,
            total_steps: 0,
            curr_step: 1
        }
    },
    props: { 
        analyzedInstructions: {
            type: Array,
            require: true
        },
        id: {
            type: String,
            require: true
        }
    },
    mounted(){

        this.getStorage();

        for (let i = 0 ; i < this.analyzedInstructions.length; i++){
                this.total_steps = this.total_steps + this.analyzedInstructions[i].steps.length;
        }
        
    },
    methods: {
        prev(){
            if (this.step - 1 < 0){
                if (this.stage > 0){
                    this.stage = this.stage - 1;
                    this.step = this.analyzedInstructions[this.stage].steps.length - 1
                }
                else{
                    return;
                }
            }
            else
                this.step = this.step - 1;
            this.curr_step = this.curr_step - 1;
        },
        next(){
            if (this.step + 1 >= this.analyzedInstructions[this.stage].steps.length){
                if (this.stage + 1 >= this.analyzedInstructions.length){
                    return;
                }
                else{
                    this.stage = this.stage + 1;
                    this.step = 0;
                }
            }
            else
                this.step = this.step + 1


            this.curr_step = this.curr_step + 1;
            this.setStorage();
            
        },
        setStorage(){

            let found = this.$root.store.recipesAtMeal.findIndex(this.check);

            if (found == -1){
                this.$root.store.recipesAtMeal.push({
                    recipe:
                    {
                        id: this.id,
                        curr_step: this.curr_step,
                        step: this.step,
                        stage: this.stage
                    }
                });
            }
            else
            {
                this.$root.store.recipesAtMeal[found].recipe.curr_step = this.curr_step;
                this.$root.store.recipesAtMeal[found].recipe.step = this.step;
                this.$root.store.recipesAtMeal[found].recipe.stage = this.stage;
            }

            found = this.$root.store.Meal.findIndex(this.check);

            if (found == -1){
                return;
            }
            else
            {
                this.$root.store.Meal[found].recipe.curr_step = this.curr_step;
                this.$root.store.Meal[found].recipe.total_step = this.total_step;
            }


        },
        getStorage(){
            console.log(this.$root.store.recipesAtMeal);
            console.log(this.id);
            let found = this.$root.store.recipesAtMeal.findIndex(this.check);
            if (found == -1)
                return;
            else{
                this.curr_step = this.$root.store.recipesAtMeal[found].recipe.curr_step;
                this.step = this.$root.store.recipesAtMeal[found].recipe.step;
                this.stage = this.$root.store.recipesAtMeal[found].recipe.stage;
            }
        },
        check(element){
            return element.recipe.id === this.id;         
        }
    }
}
</script>

<style>

</style>