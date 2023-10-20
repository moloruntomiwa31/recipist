<template>
  <div class="preloader">
    <div class="spinner"></div>
  </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.preloader {
  display: flex;
  justify-content: center;
  align-items: center;

  .spinner {
    border: 1px solid rgb(253, 249, 249);
    border-top: 3px solid #4e9f3d;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }

    100% {
      transform: rotate(360deg);
    }
  }
}
</style>
