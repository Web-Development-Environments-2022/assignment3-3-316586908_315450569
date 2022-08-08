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
          label-for="instructions"
          invalid-feedback="instructions is required"
        >
        <label for="instructions" style="font-weight: bold; text-decoration: underline; font-size:25px">Instructions</label>
        <p>Explanation : Each recipe consists of Components and each Component has steps, each step has the necessary equipments, ingredients it is made of, a description and time preparation.</p>
        <h4 style="color: red">Component {{this.analyzedInstructions.length + 1}} :</h4>
        <b-form-group
          label="Name"
          label-for="Name"
          invalid-feedback="componentName is required"
        >
          <b-form-input
            id="componentName"
            v-model="componentName"
            placeholder="Component Name"
            style="width: 170px; display:inline;"
          ></b-form-input>
        </b-form-group>
        <h5 style="color:green">Step {{this.steps.length + 1}}</h5>
          <b-form-group
          label="Equipments (Optional)"
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
            placeholder="tmp (optional)"
            style="width: 130px;display:inline;margin-left:10px "
          ></b-form-input>
          <b-form-select v-model="equipment_tmp_unit" :options="options_tmp_units" style="width:120px; margin-left:10px; height:40px; margin-bottom:5px"></b-form-select>
          <b-button @click="add_equipments" style="width: 70px;display:inline;margin-left:0px ">Add</b-button>
        </b-form-group>
        <b-form-group>
        <b-form-input
            id="step_ing_name"
            v-model="step_ing_name"
            placeholder="name of ingredient (Optional)"
            style="width: 250px; display:inline;"
          ></b-form-input>
        <b-button @click="add_ingredients" style="width: 70px;display:inline;margin-left:0px ">Add</b-button>
        </b-form-group>
        <br>
        <b-form-group>
        <textarea
            id="step_description"
            placeholder="Description Of The Step (Recommended)"
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

         <b-button @click="add_step" style="width: 100px;display:inline;margin-left:0px; background-color:green ">Add Step</b-button>
         <br>
         <br>
          <b-button @click="add_component" style="width: 150px;display:inline;margin-left:0px; background-color:red ">Add Component</b-button>

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
        steps: [],
        componentName: '',
        analyzedInstructions: []
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

        // let tmp = {
        //   name: '99999',                 
        //   readyInMinutes: '55',
        //   image: null,
        //   aggregateLikes: '99',
        //   vegan: true,
        //   vegetarian: true,
        //   glutenFree: true,
        //   analyzedInstructions: [{
        //     name: "component 1",
        //     steps: [{
        //       equipments: [{
        //           name: 'oven',
        //           tmp: {
        //             number: '200',
        //             unit: 'celcius'
        //           }
        //       }],
        //       ingredients: [{
        //         name: ''
        //       }],
        //       number: '0',
        //       step: 'prepare the bazek',
        //       length: {
        //         number: '20',
        //         unit: 'minutes'
        //     }
        //   },
        //   {
        //       equipments: [{
        //           name: 'oven2',
        //           tmp: {
        //             number: '200',
        //             unit: 'celcius'
        //           }
        //       }],
        //       ingredients: [{
        //         name: ''
        //       }],
        //       number: '1',
        //       step: 'prepare the bazek2',
        //       length: {
        //         number: '20',
        //         unit: 'minutes'
        //     }
        //   }
        //   ]},
        //   {
        //     name: "component 2",
        //     steps: [{
        //       equipments: [{
        //           name: 'magash',
        //           tmp: {
        //             number: '',
        //             unit: ''
        //           }
        //       }],
        //       ingredients: [{
        //         name: 'tomato'
        //       },
        //       {
        //         name: 'olives'
        //       }],
        //       number: '0',
        //       step: 'prepare the pizza',
        //       length: {
        //         number: '20',
        //         unit: 'minutes'
        //     }
        //   },
        //   {
        //       equipments: [],
        //       ingredients: [],
        //       number: '1',
        //       step: 'insert the pizza',
        //       length: {
        //         number: '10',
        //         unit: 'minutes'
        //     }
        //   }
        //   ]}
        //   ],
        //   ingredients: [{
        //     name: 'kemah',
        //     amount: '500',
        //     units: 'grams'
        // },{
        //     name: 'tomato',
        //     amount: '50',
        //     units: 'grams'
        // },
        // {
        //   name: 'cheese',
        //   amount: '500',
        //   units: 'grams'
        // }
        // ],
        //   servings: '2'
        //   }


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
            this.$root.store.server_domain + "/users/createRecipe/" + this.name,
            {
              params: {
                  name: this.$route.params.query,                 
                  readyInMinutes: this.time,
                  image: this.url,
                  aggregateLikes: this.likes,
                  vegan: this.vegan,
                  vegetarian: this.vegetarian,
                  glutenFree: this.gluten,
                  instructions: this.analyzedInstructions,
                  ingredients: this.ingredients,
                  servings: this.servings
                }
              }
          );
          // this.response = await this.axios.post(
          //   this.$root.store.server_domain + "/users/createRecipe/" + tmp.name,
          //   {
          //     params: {
          //         name: this.$route.params.query,                 
          //         readyInMinutes: tmp.time,
          //         image: tmp.url,
          //         aggregateLikes: tmp.likes,
          //         vegan: tmp.vegan,
          //         vegetarian: tmp.vegetarian,
          //         glutenFree: tmp.gluten,
          //         instructions: tmp.analyzedInstructions,
          //         ingredients: tmp.ingredients,
          //         servings: tmp.servings
          //       }
          //     }
          // );
          this.analyzedInstructions = [];
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
      },
      add_component(){
        this.analyzedInstructions.push({
          name: this.componentName,
          steps: this.steps
        });
        this.componentName = '';
        this.steps = [];
      }
    }
  }
</script>
<style>

</style>
