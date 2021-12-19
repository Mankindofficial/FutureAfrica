<template>
  <div class="homepage">
    <div class="mb-5">
      <h1 class="homepage_title">Future Africa Frontend Engineering Challenge</h1>
      <p class="homepage_text">Click the button below to start Quiz.</p>
      <b-button class="my-4 navigation_button_inverse" @click="$router.push({ name: 'questions' })">Start Quiz</b-button>
    </div>
  </div>
</template>

<style>
  :root {
    --primary-color: #3CAC70;
    --secondary-color: #FBBB07;
  }
  body {
    font-family: 'Roboto', sans-serif !important;
  }
  .homepage {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    background-color: var(--primary-color);
  }
  .homepage_title {
    font-weight: 600;
    max-width: 700px;
    line-height: 3.5rem;
    margin-bottom: 3rem;
  }
  .homepage_text {
    font-size: 1.2rem;
  }
  .navigation_button {
    border-color: var(--primary-color);
    background-color: var(--primary-color);
  }
  .navigation_button_inverse {
    border-color: var(--secondary-color);
    background-color: var(--secondary-color);
  }
</style>

<script>
export default {
  name: 'App',
}
</script>
