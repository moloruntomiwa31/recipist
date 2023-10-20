<template>
  <div v-for="recipe in recipes" :key="recipe.id" class="recipe">
    <div class="recipe-img">
      <img
        :src="`https://spoonacular.com/recipeImages/${recipe.image}`"
        :alt="recipe.title"
      />
    </div>
    <div class="info">
      <h3 class="recipe-title">{{ recipe.title }}</h3>
      <button @click="router.push(`/recipes/${recipe.id}`)">
        Get more info
      </button>
    </div>
    <div class="serving-time">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
      >
        <g fill="none">
          <path
            d="M24 0v24H0V0h24ZM12.593 23.258l-.011.002l-.071.035l-.02.004l-.014-.004l-.071-.035c-.01-.004-.019-.001-.024.005l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427c-.002-.01-.009-.017-.017-.018Zm.265-.113l-.013.002l-.185.093l-.01.01l-.003.011l.018.43l.005.012l.008.007l.201.093c.012.004.023 0 .029-.008l.004-.014l-.034-.614c-.003-.012-.01-.02-.02-.022Zm-.715.002a.023.023 0 0 0-.027.006l-.006.014l-.034.614c0 .012.007.02.017.024l.015-.002l.201-.093l.01-.008l.004-.011l.017-.43l-.003-.012l-.01-.01l-.184-.092Z"
          />
          <path
            fill="currentColor"
            d="M12 2c5.523 0 10 4.477 10 10s-4.477 10-10 10S2 17.523 2 12S6.477 2 12 2Zm0 4a1 1 0 0 0-1 1v5a1 1 0 0 0 .293.707l3 3a1 1 0 0 0 1.414-1.414L13 11.586V7a1 1 0 0 0-1-1Z"
          />
        </g>
      </svg>
      <p class="time">{{ recipe.readyInMinutes }}mins</p>
    </div>
  </div>
</template>

<script setup>
defineProps(["recipes"])
const router = useRouter()
</script>

<style lang="scss" scoped>
.recipe {
  height: 400px;
  box-shadow: 0px 0px 3px;
  width: 100%;
  max-width: 500px;
  position: relative;

  .recipe-img {
    img {
      height: 200px;
      width: 100%;
      object-fit: cover;
    }
  }
  .info {
    padding: 1rem;
    .recipe-title {
      font-size: 1.2rem;
      margin: 16px 0;
    }
  }

  .serving-time {
    position: absolute;
    background-color: #4e9f3d;
    border-radius: 0 0 6px 0;
    padding: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    top: 0;
    left: 0;
    color: white;
  }
}
</style>
