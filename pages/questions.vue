<template>
  <div class="container">
    <h2 class="my-4">Questions</h2>
    <ul class="questions_list">
      <li v-for="(question, index) in questions" :key="question.questionText" v-bind:class="[!selected[index] && error] + ' mb-4'">
        <div class="question_title">
          {{index + 1}}. {{ question.questionText }}
        </div>
        <b-form-group v-slot="{ ariaDescribedby }" class="my-2">
          <div v-for="option in question.answerOptions" :key="option.answerText">
            <b-form-radio v-model="selected[index]" :aria-describedby="ariaDescribedby" :name="question.questionText" :value="option">{{ option.answerText }}</b-form-radio>
          </div>
        </b-form-group>
      </li>
    </ul>
    <div class="text-center mt-4 mb-3">
      <b-button class="navigation_button" @click="submit">Submit</b-button>
    </div>
  </div>
</template>


<script>
import questions from '~/static/questions.json';
export default {
	name: 'QuestionsPage',
	data: function() {
		return {
      selected: [],
      error: null,
		}
	},
  asyncData: function() {
    return { questions }
  },
	methods: {
		submit: function() {
      const answered = this.selected.filter(item => !!item);
      if (answered.length !== this.questions.length) {
        this.error = 'error';
        alert("Please answer all the questions");
      } else {
        this.error = null;
        this.$router.push({ name: 'results', params: { data: this.selected } });
      }
    }
  }
}
</script>


<style scoped>
  .questions_list {
    list-style: none;
    padding: 0px;
  }
  .error {
    color: red;
  }
  .question_title {
    padding: 0.5rem;
    background-color: #f4f4f4;
    border-left: 4px solid var(--secondary-color);
  }
  .custom-control-input:checked ~ .custom-control-label::before {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
  }
</style>
