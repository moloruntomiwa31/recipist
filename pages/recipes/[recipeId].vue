<template>
  <div class="specific-recipe">
    <button @click="router.back()" class="router-btn">Back</button>
    <div class="recipe-details">
      <div class="recipe-img">
        <img :src="recipe.image" :alt="recipe.title" />
      </div>
      <div class="info">
        <h1>{{ recipe.title }}</h1>
        <p><span>Time to cook: </span>{{ recipe.readyInMinutes }}mins</p>
        <div class="ingredients">
          <h3>Ingredients</h3>
          <ul class="ingredients-chips">
            <li v-for="ingredient in recipe.extendedIngredients">
              {{ ingredient.name }}
            </li>
          </ul>
        </div>
        <div class="instruction">
          <h3>Instructions</h3>
          <p
            class="instruction-text"
          >{{ recipe.instructions }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const router = useRouter();
const recipe = ref(null);
const { data } = await useFetch(
  `https://api.spoonacular.com/recipes/${route.params.recipeId}/information`,
  {
    query: {
      apiKey: "7805e5f1b82b440b9ad649c9018d0609",
    },
  }
);
recipe.value = data.value;
console.log(recipe.value);

useHead({
    title: `Recipist | ${recipe.value.title}`,
    meta: [
    { name: 'description', content: `${recipe.value.summary}` }
  ],
})
</script>

<style lang="scss" scoped>
.specific-recipe {
  .router-btn {
    justify-self: center;
  }

  .recipe-details {
    display: flex;
    flex-direction: column;
    gap: 2rem;
    min-width: 100%;

    @media screen and (min-width: 964px) {
      flex-direction: row;
    }

    .recipe-img {
      width: 100%;
      max-width: 400px img {
        width: 100%;
        height: auto;
      }
    }

    .info {
      width: 100%;
      max-width: 700px;
      margin: 2rem;

      p{
        font-size: 1.3rem;
        margin: 10px 0;
      }
      h3 {
        text-align: center;
        font-size: 1.35rem;
      }
      h1 {
        font-size: 2.4rem;
      }
      .ingredients {
        ul {
          display: grid;
          gap: 10px;
          grid-template-columns: repeat(1fr);
          @media (min-width: 500px) {
            grid-template-columns: repeat(2, 1fr);
          }
          @media (min-width: 750px) {
            grid-template-columns: repeat(3, 1fr);
          }
          li {
            text-transform: capitalize;
            font-size: 1.5rem;
            margin-left: 10px;
          }
        }
      }
      .instruction {
        font-size: 1.3rem;
      }
    }
  }
}
</style>
