<template>
  <div>
    <!-- Hero -->
    <Hero @searchRecipes="searchRecipes" @clearSearch="clearSearch"  :searchedRecipeResult="result"/>

    <!-- Searched Results -->
    <div class="loading" v-if="pending">
      <Loading />
    </div>

    <div v-else>
      <div v-if="result.length > 0">
        <div class="category">
          <h2>Searched Recipes</h2>
        </div>
        <div class="recipes">
          <SearchedRecipeCard  :result="result"/>
        </div>
      </div>

      <!-- Popular Recipes -->
      <div id="popular-recipes" v-else>
        <div class="category">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 16 16"
          >
            <path
              fill="currentColor"
              d="M3.75 10.999h4.5a.75.75 0 0 1 .102 1.493l-.102.007h-4.5a.75.75 0 0 1-.102-1.493l.102-.007h4.5h-4.5Zm1.47-5.78a.75.75 0 0 1 .976-.072l.084.073l3.5 3.5a.75.75 0 0 1-.976 1.133L8.72 9.78l-3.5-3.5a.75.75 0 0 1 0-1.06ZM11.75 3a.75.75 0 0 1 .743.648l.007.102v4.5a.75.75 0 0 1-1.493.102L11 8.25v-4.5a.75.75 0 0 1 .75-.75Z"
            />
          </svg>
          <h2>Popular Recipes</h2>
        </div>
        <div class="recipes">
          <RecipeCard :recipes="recipes.results" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const result = ref([]);
const router = useRouter();

const { data: recipes, pending } = await useLazyFetch(
  "https://api.spoonacular.com/recipes/search",
  {
    query: {
      apiKey: "7805e5f1b82b440b9ad649c9018d0609",
      sort: "popularity",
    },
    server: false,
  }
);

const searchRecipes = async (dish) => {
  const { data } = await useLazyFetch(
    "https://api.spoonacular.com/recipes/complexSearch",
    {
      query: {
        apiKey: "7805e5f1b82b440b9ad649c9018d0609",
        query: dish,
      },
    }
  );
  result.value = toRaw(data.value.results);
  console.log(result.value);
};

const clearSearch = () => {
  result.value = [];
};
</script>

<style lang="scss" scoped>
.category {
  text-align: center;
  position: relative;

  svg {
    position: absolute;
    top: 0;
    left: 20%;

    @media screen and (min-width: 640px) {
      left: 35%;
    }
    @media screen and (min-width: 946px) {
      left: 40%;
    }
  }
}

.recipes {
  display: grid;
  column-gap: 32px;
  row-gap: 64px;
  grid-template-columns: 1fr;
  padding: 2rem;
  @media (min-width: 500px) {
    grid-template-columns: repeat(2, 1fr);
  }
  @media (min-width: 750px) {
    grid-template-columns: repeat(3, 1fr);
  }
  @media (min-width: 1100px) {
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>
