<template>
  <div class="container">
    <div v-if="answers.length > 0">
      <h3 class="mt-5 mb-4">Your answers were submitted successfully.</h3>
      <div>
        <p>You scored {{ score }} out of {{ answers.length }}</p>
      </div>
    </div>    
    <h3 v-else class="mt-5 mb-4">Your record has been cleared.</h3>
    <div>
      <b-button class="my-4 navigation_button" @click="$router.push({ name: 'index' })">Back to home</b-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ResultPage',
  computed: {
    answers: function() {
      return this.$route.params.data || [];
    },
    score: function() {
      return this.answers.filter(item => item.isCorrect).length;
    }
  }
}
</script>
