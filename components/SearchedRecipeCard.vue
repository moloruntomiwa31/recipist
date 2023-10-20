<template>
  <div v-for="recipe in result" :key="recipe.id" class="searchedRecipe">
    <img :src="recipe.image" :alt="recipe.id" />
    <h2>{{ recipe.title }}</h2>
    <button @click="router.push(`/recipes/${recipe.id}`)">Get more info</button>
  </div>
</template>

<script setup>
defineProps(["result"]);
const router = useRouter();
</script>

<style lang="scss" scoped>
.searchedRecipe {
  height: 450px;
  box-shadow: 0px 0px 3px;
  padding: 1rem;
  width: 100%;
  max-width: 500px;

  img {
    height: 200px;
    width: 100%;
    object-fit: cover;
  }

  button {
    margin: 10px 0;
  }
}
</style>
