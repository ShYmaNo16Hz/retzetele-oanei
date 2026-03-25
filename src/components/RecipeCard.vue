<template>
  <div class="card shadow-sm border-0 rounded-4 overflow-hidden">
    <!-- Header -->
    <div class="card-header bg-success bg-gradient text-white border-0 py-2 px-4 position-relative">
      <h5 class="card-title mb-1 fw-bold">
        {{ recipe.name }}
      </h5>
      <div class="row align-items-center">
        <div class="col">
          <div class="badge bg-white text-success rounded-pill fs-7">
            🍽️ {{ recipe.servings }} porție
          </div>
        </div>
        <div class="col-auto">
          <span class="badge bg-black bg-opacity-50 rounded-pill rounded-pill">
            {{ recipe.category }}
          </span>
        </div>
      </div>
    </div>

    <div class="card-body px-2 pb-3 pt-2">
      <!-- Macros -->
      <div class="row g-2 mb-2">
        <div class="col-4" v-for="(macro, key) in recipe.macros" :key="key">
          <div class="text-center p-2 rounded-3" :class="macroClass(key)">
            <div class="fw-bold fs-6">{{ macro.grams }}g</div>
            <small class="text-muted text-capitalize">{{ macroLabel(key) }}</small>
            <div>
              <span class="badge rounded-pill" :class="macroBadgeClass(key)">
                {{ macro.percentage }}%
              </span>
            </div>
          </div>
        </div>
      </div>

      <!-- Ingredients -->
      <h6 class="fw-bold mb-2"><span class="me-1">🥗</span> Ingrediente</h6>
      <ul class="list-group list-group-flush mb-2">
        <li
          v-for="(ing, i) in recipe.ingredients"
          :key="i"
          class="list-group-item d-flex justify-content-between align-items-center px-0 border-bottom"
          style="padding: 6px 0px"
        >
          <small>{{ ing.name }} </small>
          <span class="badge bg-light text-dark rounded-pill" style="font-size: 12px">
            {{ ing.amount_grams }}g
          </span>
        </li>
      </ul>

      <!-- Instructions -->
      <h6 class="fw-bold mb-2"><span class="me-1">📝</span> Instrucțiuni</h6>
      <p class="text-muted small lh-lg mb-0">{{ recipe.instructions }}</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  recipe: {
    type: Object,
    required: true,
    default: () => ({
      id: 1,
      name: 'Quesadilla cu pui',
      category: 'Pranz / Cina',
      prep_time_minutes: null,
      servings: 1,
      ingredients: [
        { amount_grams: 50, name: 'Lipie libaneza Zaman' },
        { amount_grams: 30, name: 'Soft cheese Light - Milbona' },
        { amount_grams: 40, name: 'Avocado' },
        { amount_grams: 30, name: 'Porumb dulce - Sweetcorn - Freshona' },
        { amount_grams: 15, name: 'Branza Cheddar' },
        { amount_grams: 110, name: 'Piept de pui - Lidl' },
      ],
      instructions: 'Pieptul de pui se asezoneaza dupa gust si se gateste fara grasime...',
      macros: {
        protein: { percentage: 35, grams: 38.09 },
        carbohydrates: { percentage: 35, grams: 37.97 },
        fat: { percentage: 30, grams: 14.99 },
      },
    }),
  },
})

const macroLabel = (key) => {
  const labels = { protein: 'Proteine', carbohydrates: 'Carbohidrați', fat: 'Grăsimi' }
  return labels[key] || key
}

const macroClass = (key) => {
  const classes = {
    protein: 'bg-primary bg-opacity-10',
    carbohydrates: 'bg-warning bg-opacity-10',
    fat: 'bg-danger bg-opacity-10',
  }
  return classes[key]
}

const macroBadgeClass = (key) => {
  const classes = {
    protein: 'bg-primary',
    carbohydrates: 'bg-warning text-dark',
    fat: 'bg-danger',
  }
  return classes[key]
}
</script>
<style scoped>
.category-position {
  position: absolute;
  top: 0.75rem;
  right: 0.75rem;
}
</style>
