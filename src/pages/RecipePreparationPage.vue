<template>
    <div>

    </div>
</template>

<script>
export default {
    name: "RecipePreparationPage",
    data(){
        return {
            recipeIngredients: [],
            analyzedInstructions: [],
            id: ''
        }
    },
    async mounted(){
        console.log(this.$route.params.id);
        const response = await this.axios.get(this.$root.store.server_domain + "/recipes/" + `${this.$route.params.id}` +"/analyzedInstructions");
        console.log(response.data); // its working

    }
}
</script>

<style>

</style>