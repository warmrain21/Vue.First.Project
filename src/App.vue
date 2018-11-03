<template>
  <div id="app">
    <nav-bar></nav-bar>
    <h1>Hello Word</h1>
    <button class="btn btn-success" @click="isNew = !isNew">
      Create
    </button>
    <recipe-form v-if="isNew" @saveRecipe="addRecipe"/>
    <div class="form-group row">
        <label class="col-md-4 control-label">Search</label>
        <div class="col-md-5">
            <input type="text" class="form-control" v-model="searchtext">
        </div>
    </div>
    <ul>
      <li v-for="(recipe, index) in filterList" :key="index+recipe.title">
        {{ recipe.title }}
      </li>
    </ul>
  </div>
</template>




<script>
import NavBar from './layout/navbar.vue'
import RecipeForm from './components/RecipeForm.vue'



export default {
  name: 'app',
  components: {
    NavBar,
    RecipeForm
  },
  data () {
    return {
      recipes: [],
      isNew: false,
      searchtext: ''
    }
  },
  mounted() 
  {
    if(localStorage.getItem('recipe')) {
      this.recipes = JSON.parse(localStorage.getItem('recipes'))
    }
  },
  computed: {
    filterList() {
      return this.recipes.filter(recipe => {
        return recipe.title.toLowerCase().indexOf(this.searchtext.toLowerCase()) > -1
      })
    }
  },
  methods: {
    setLocalStorage () {
      localStorage.setItem('recipes', JSON.stringify(this.recipes))
    },
    addRecipe (recipe) {
      this.recipes.push(recipe)
      this.setLocalStorage()
      this.isNew = false
    },
    searchRecipe()
    {
      this.recipes = this.recipes.filter((recipe) => {
        return recipe.title.toLowerCase().indexOf(this.searchtext.toLowerCase()) > -1
      })
    }
  }
}
</script>



<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
