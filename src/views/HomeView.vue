<template>
  <div class="container">
    <h5 class="text-center">Rețetele Oanei PDR</h5>
    <div class="row">
      <div class="col-12" v-for="(item, index) in recipes" :key="index">
        <RecipeCard :recipe="item" />
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
    }
  },
  created() {
    console.log(this.recipes)
  },
}
</script>
