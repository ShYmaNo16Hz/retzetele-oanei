<template>
  <div class="container">
    <h5 class="text-center">{{ recipes.length }} rețete ale Oanei PDR</h5>
    <input
      v-model="search"
      type="text"
      placeholder="Caută rețetele, pregătaro..."
      class="form-control form-control-sm"
    />
    <div class="row mt-3">
      <div class="col-12 mb-3" v-for="(item, index) in filteredRecipes" :key="index">
        <RecipeCard :recipe="item" />
      </div>
    </div>
    <div class="mt-3" v-if="!filteredRecipes.length">
      <div class="text-center mt-5">
        <img src="@/assets/not-found.png" alt="Dish not found" />
        <h5 class="mt-2 text-secondary">Ceea ce ai căutat nu există (;</h5>
      </div>
    </div>
  </div>
</template>
<script>
import RecipeCard from '@/components/RecipeCard.vue'
import recipes from '@/assets/recipes.json'
export default {
  components: {
    RecipeCard,
  },
  data() {
    return {
      recipes,
      search: '',
    }
  },
  computed: {
    filteredRecipes() {
      const q = this.search.toLowerCase().trim()
      if (!q) return this.recipes
      return this.recipes.filter(
        (recipe) =>
          recipe.name.toLowerCase().includes(q) ||
          recipe.ingredients.some((i) => i.name.toLowerCase().includes(q)),
      )
    },
  },
  created() {
    console.log(this.recipes)
  },
}
</script>
