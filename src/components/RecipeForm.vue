<template>
    <div>
        <form @submit.prevent="" class="form-horizontal">
            <fieldset>
                <!-- Form Name -->
                <legend>Recipe Form</legend>
                <!-- Text input-->
                <div class="form-group row">
                    <label class="col-md-4 control-label" for="title">Title</label>
                    <div class="col-md-5">
                        <input id="title" name="title" v-model="recipe.title"  type="text" placeholder="" class="form-control input-md">
                    </div>
                </div>

                <!-- Text input-->
                <div class="form-group row">
                    <label class="col-md-4 control-label" for="img_url">image URL</label>
                    <div class="col-md-5">
                        <input id="img_url" name="img_url" v-model="recipe.image_url" type="text" placeholder="" class="form-control input-md">
                    </div>
                </div>

                <!-- Text input-->
                <div class="form-group row">
                    <label class="col-md-4 control-label" for="description">Description</label>
                    <div class="col-md-5">
                        <input id="description" name="description" v-model="recipe.description" ype="text" placeholder="" class="form-control input-md">
                    </div>
                </div>

                <div class="form-group row row">
                    <div class="col">
                        <button class="btn btn-primary" @click="addIngredient">
                            <i class="fa fa-plus-circle"></i> more Ingredient
                        </button>
                    </div>
                </div>
                
                <!-- Text input-->
                <div class="form-group row" style="margin-top: 15px;">
                    <label class="col-md-4 control-label" for="ingredien">Ingredient</label>
                    <div class="col-md-5">
                        <div v-for="(ingredient, index) in recipe.ingredient" :key="index">
                            <input v-model="recipe.ingredient[index]" style="margin-buttom: 15px" id="ingredient" name="ingredient" type="text" placeholder="" class="form-control input-md">
                        </div>
                    </div>
                </div>

                <!-- Button (Double) -->
                <div class="form-group row">
                    <label class="col-md-4 control-label" for="btnSubmit"></label>
                    <div class="col-md-8">
                        <button id="btnSubmit" @click="save" name="btnSubmit" class="btn btn-success">Submit</button>
                        <button id="btnCancel" name="btnCancel" class="btn btn-danger">Cancel</button>
                    </div>
                </div>

            </fieldset>
        </form>
    </div>
</template>

<script>
export default {
    data(){
        return {
            recipe: {
                title: '',
                description: '',
                image_url: '',
                ingredient: ['']
            }
        }
    },
    methods: {
        addIngredient(){
            this.recipe.ingredient.push('')
        },
        save(){
            this.$emit('saveRecipe', this.recipe)
        }
    }
}
</script>
<style scoped>
</style>