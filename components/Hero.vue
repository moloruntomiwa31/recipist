<template>
  <div class="hero">
    <div class="hero-img">
      <img src="~/assets/img/heroFood.png" alt="hero-image" class="img-fluid" />
    </div>
    <div class="hero-text">
      <h1 class="hero-text-title">
        Find the perfect recipes <span>everyday.</span>
      </h1>
      <p class="hero-text-details">
        More than 20 thousand recipes of healthy food.
      </p>
      <div class="link">
        <a href="#popular-recipes">View Popular</a>
      </div>
      <div class="search">
        <input
          type="text"
          class="search-input"
          placeholder="Search for recipes here..."
          v-model.lazy="searchInput"
          @keyup.enter="searchRecipes"
        />
        <button class="btn" @click="clearSearch" v-show="searchInput !== ''">
          Clear
        </button>
      </div>
      <div v-if="errorMessage">Recipe not found.</div>
    </div>
  </div>
</template>

<script setup>
const searchInput = ref("");
const emit = defineEmits(["searchRecipes", "clearSearch"]);
const props = defineProps({
  searchedRecipeResult: Array
})

const searchRecipes = () => {
  emit("searchRecipes", searchInput.value);
};
const clearSearch = () => {
    emit("clearSearch");
    searchInput.value = ''
};

const errorMessage = computed(() => {
  return props.searchedRecipeResult.length < 1 && searchInput.value !== '' 
})
</script>

<style lang="scss" scoped>
.hero {
  display: flex;
  flex-direction: row-reverse;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  min-height: 60vh;

  @media screen and (max-width: 640px) {
    flex-direction: column;
  }

  .hero-img {
    img {
      max-height: 500px;
      width: 100%;

      @media (min-width: 800px) {
        max-height: 500px;
        width: initial;
      }
    }
  }
  .hero-text {
    text-align: center;
    max-width: 500px;
    @media screen and (min-width: 640px) {
      text-align: left;
    }
    .link {
      margin: 10px 0;
      a {
        text-decoration: none;
        color: #4e9f3d;
        border-radius: 5px;
        font-size: 1.2rem;
      }
    }
    .hero-text-title {
      font-size: 3rem;
      font-weight: 600;

      span {
        color: #4e9f3d;
      }
    }
    .hero-text-details {
      font-size: 1.5rem;
    }
  }

  .search {
    margin: 2rem 0;
    white-space: nowrap;
    .search-input {
      padding: 1rem;
      border-radius: 10px 0 0 10px;
      border: none;
      background-color: #d8e9a8;
      font-size: 1.2rem;

      &:focus {
        outline: none;
      }
    }
  }
}
</style>
