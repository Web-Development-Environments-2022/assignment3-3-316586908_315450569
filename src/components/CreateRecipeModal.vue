<template>
  <div>
    <b-modal
      id="modal-prevent-closing"
      ref="modal"
      title="Create Your Recipe"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
          label="Recipe Name"
          label-for="name-input"
          invalid-feedback="Name is required"
          :state="nameState"
        >
          <b-form-input
            id="name-input"
            v-model="name"
            :state="nameState"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group
          label="URL Of Picture"
          label-for="url"
          invalid-feedback="url is required"
          :state="nameState"
        >
         <b-form-input
            id="url"
            v-model="url"
            :state="nameState"
            required
          ></b-form-input>
        
        </b-form-group>
        <b-form-group
          label="Ready In Minutes"
          label-for="ready"
          invalid-feedback="time is required"
          :state="nameState"
        >
          <b-form-input
            id="ready"
            v-model="time"
            :state="nameState"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group
          label="Popularity"
          label-for="popularity"
          invalid-feedback="popularity is required"
          :state="nameState"
        >
          <b-form-input
            id="popularity"
            v-model="likes"
            placeholder="Insert number of likes to the picture"
            :state="nameState"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group
          label="Vegan / Vegetarian / None"
          invalid-feedback="value is required"
          :state="nameState"
        >
          <b-form-select v-model="vegan" :options="options_v" style="width:150px; margin-left:0px; height:40px; margin-bottom:5px"></b-form-select>
        </b-form-group>
        <b-form-group
          label="Gluten Free"
          label-for="name-input"
          invalid-feedback="value is required"
          :state="nameState"
        >
        <b-form-select v-model="gluten" :options="options_g" style="width:150px; margin-left:0px; height:40px; margin-bottom:5px"></b-form-select>
        </b-form-group>
        <b-form-group
          label="Ingredients"
          label-for="name-input"
          invalid-feedback="value is required"
          :state="nameState"
        >
          <b-form-input
            id="ing-name"
            v-model="ing_name"
            :state="nameState"
            placeholder="name"
            
            style="width: 150px; display:inline;"
          ></b-form-input>
          <b-form-input
            id="ing-amount"
            v-model="ing_amount"
            :state="nameState"
            
            placeholder="amount"
            style="width: 100px;display:inline;margin-left:10px "
          ></b-form-input>
        
        <b-form-select v-model="ing_unit" :options="options" style="width:150px; margin-left:10px; height:40px; margin-bottom:5px"></b-form-select>
          <b-button @click="add" style="width: 70px;display:inline;margin-left:0px ">Add</b-button>
        </b-form-group>
        <b-form-group
          label="Servings"
          label-for="servings"
          invalid-feedback="servings is required"
          :state="nameState"
        >
          <b-form-input
            id="servings"
            v-model="servings"
            placeholder="Insert number of servings"
            :state="nameState"
            required
          ></b-form-input>
        </b-form-group>
        </form>
        <b-form-group
          label="Instructions"
          label-for="instructions"
          invalid-feedback="instructions is required"
        >
        <h5>Step {{this.steps.length + 1}}</h5>
          <b-form-group
          label="Equipments"
          label-for="Equipments"
          invalid-feedback="Equipments is required"
        >
          <b-form-input
            id="equipment_name"
            v-model="equipment_name"
            placeholder="name of equipment"
            style="width: 170px; display:inline;"
          ></b-form-input>
          <b-form-input
            id="equipment_tmp_num"
            v-model="equipment_tmp_num"
            placeholder="tmp"
            style="width: 100px;display:inline;margin-left:10px "
          ></b-form-input>
          <b-form-select v-model="equipment_tmp_unit" :options="options_tmp_units" style="width:150px; margin-left:10px; height:40px; margin-bottom:5px"></b-form-select>
          <b-button @click="add_equipments" style="width: 70px;display:inline;margin-left:0px ">Add</b-button>
        </b-form-group>
        <b-form-group>
        <b-form-input
            id="step_ing_name"
            v-model="step_ing_name"
            placeholder="name of ingredient"
            style="width: 200px; display:inline;"
          ></b-form-input>
        <b-button @click="add_ingredients" style="width: 70px;display:inline;margin-left:0px ">Add</b-button>
        </b-form-group>
        <br>
        <b-form-group>
        <textarea
            id="step_description"
            placeholder="Description Of The Step"
            v-model="step_description"
            required
            style="width:400px;height:100px"
          ></textarea>
          </b-form-group>
          <b-form-group
          label="Preparation time of the step (Optional)"
          label-for="Length"
          >
          <b-form-input
            id="length_num"
            v-model="length_num"
            placeholder="minutes"
            style="width: 150px; display:inline;"
          ></b-form-input>
          </b-form-group>

         <b-button @click="add_step" style="width: 100px;display:inline;margin-left:0px ">Add Step</b-button>
        </b-form-group>
      
    </b-modal>
  </div>
</template>

<script>
export default {
    data() {
      return {
        name: '',
        url:'',
        time:'',
        likes:'',
        vegan: false,
        vegetarian: false,
        gluten: '',
        ing_name:'',
        ing_amount:'',
        ing_unit: '',
        instructions: '',
        servings: '',
        ingredients: [],
        options_v: [
          {value: false, text: 'None'},
          {value: 'vegan', text: 'vegan'},
          {value: 'vegetarian', text: 'vegetarian'}
        ],
        options_g: [
          {value: true, text: 'Yes'},
          {value: false, text: 'No'}
        ],
        options: [
          { value: '', text: 'No Units'},
          { value: 'tbsps', text: 'tablespoons' },
          { value: 'tsps', text: 'teaspoons' },
          { value: 'gram', text: 'grams' },
          { value: 'cups', text: 'cups' },
          { value: 'pinch', text: 'pinchs' },
          { value: 'ml', text: 'milliliters' },
          { value: 'oz', text: 'ounces' }
        ],
        options_tmp_units: [
          { value: 'celsius', text: 'celsius' },
          { value: 'fahrenheit', text: 'fahrenheit' }
        ],
        nameState: null,
        submittedNames: [],
        equipment_name: '',
        equipment_tmp_num: '',
        equipment_tmp_unit: '',
        equipments: [],
        step_ingredients: [],
        step_ing_name: '',
        step_description: '',
        length_num: '',
        steps: []
      }
    },
    methods: {
      checkFormValidity() {
        const valid = this.$refs.form.checkValidity()
        this.nameState = valid
        return valid
      },
      resetModal() {
        this.name= '';
        this.url='';
        this.time='';
        this.likes='';
        this.vegan=false;
        this.vegetarian = false;
        this.gluten='';
        this.ing_name='';
        this.ing_amount='';
        this.ing_unit= '';
        this.instructions = '';
        this.servings = '';
        this.ingredients= [];
        this.nameState = null
      },
      handleOk(bvModalEvent) {
        // Prevent modal from closing
        bvModalEvent.preventDefault()
        // Trigger submit handler
        this.handleSubmit()
      },
      async handleSubmit() {
        // Exit when the form isn't valid
        if (!this.checkFormValidity()) {
          return
        }
        
        if (this.vegan == 'vegan')
        {
          this.vegan = true;
          this.vegetarian = true;
        }
        else if (this.vegan == 'vegetarian')
        {
          this.vegan = false;
          this.vegetarian = true;
        }
        else
        {
          this.vegan = false;
          this.vegetarian = false;
        }
        // create http request to the server 
        try {
          this.response = await this.axios.post(
            // "https://test-for-3-2.herokuapp.com/recipes/info",
            // this.$root.store.server_domain + "/recipes/info",document.getElementById("search_input").value
            this.$root.store.server_domain + "/users/createRecipe/" + this.name,
            //  + "/" + this.number + "/" + this.cuisine + "/" + this.diet + "/" + this.intolerance + "/" + this.sort,
            {
              params: {
                  name: this.$route.params.query,                 
                  readyInMinutes: this.time,
                  image: this.url,
                  aggregateLikes: this.likes,
                  vegan: this.vegan,
                  vegetarian: this.vegetarian,
                  glutenFree: this.gluten,
                  instructions: this.steps,
                  ingredients: this.ingredients,
                  servings: this.servings
                }
              }
          );
          this.steps = [];
          // console.log(this.response.data, "HERLLO");
          // console.log("response.status", this.response.status, this.response.length);
          if (this.response.status !== 200) this.$router.replace("/NotFound");
        } catch (error) {
          console.log("error.response.status", error.response.status);
          this.$router.replace("/NotFound");
          return;
        }
        
        // Hide the modal manually
        this.$nextTick(() => {
          this.$bvModal.hide('modal-prevent-closing')
        })
      },
      add(){
        this.ingredients.push({
          name: this.ing_name,
          amount: this.ing_amount,
          units: this.ing_unit
        });
        this.ing_name = '';
        this.ing_amount = '';
        this.ing_unit = '';
      },
      add_equipments(){
        this.equipments.push({
          name: this.equipment_name,
          tmp: {
            number: this.equipment_tmp_num,
            unit: this.equipment_tmp_unit
          }
        });
        this.equipment_name = '';
        this.equipment_tmp_num = '';
        this.equipment_tmp_unit = '';
      },
      add_ingredients(){
        this.step_ingredients.push({
          name: this.step_ing_name
        });
        this.step_ing_name = '';
      },
      add_step(){
        this.steps.push({
          equipments: this.equipments,
          ingredients: this.step_ingredients,
          number: this.steps.length + 1,
          step: this.step_description,
          length: {
            number: this.length_num,
            unit: 'minutes'
          }
        });
        this.equipments = [];
        this.step_ingredients = [];
        this.step_description = '';
        this.length_num = '';
      }
    }
  }
</script>
<style>

</style>
