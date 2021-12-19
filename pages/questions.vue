<template>
  <div class="container">
    <h2 class="questions_header">Questions</h2>
    <ul class="questions_list">
      <li v-for="(question, index) in questions" :key="question.questionText" v-bind:class="[!selected[index] && error] + ' questions_list_item'">
        <div class="question_title">
          {{index + 1}}. {{ question.questionText }}
        </div>
        <b-form-group v-slot="{ ariaDescribedby }" class="question_options">
          <div v-for="option in question.answerOptions" :key="option.answerText">
            <b-form-radio v-model="selected[index]" :aria-describedby="ariaDescribedby" :name="question.questionText" :value="option">{{ option.answerText }}</b-form-radio>
          </div>
        </b-form-group>
      </li>
    </ul>
    <div class="questions_button_wrapper">
      <b-button class="questions_buttons" @click="submit">Submit</b-button>
    </div>
  </div>
</template>


<script>
import questions from '~/static/questions.json';
export default {
	name: 'Questions',
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
    formatData: function(data) {
      return JSON.parse(JSON.stringify(data));
    },
		submit: function() {
      const answered = this.selected.filter(item => !!item);
      if (answered.length !== this.questions.length) {
        this.error = 'error';
        alert("Please answer all the questions");
      } else {
        this.error = null;
        // this.$router.push({ name: 'results', params: { data: this.formatData(this.selected) } });
      }
    }
  }
}
</script>


<style>
  .questions_header {
   margin: 1rem 0 1.5rem; 
  }
  .questions_list {
    list-style: none;
    padding: 0px;
  }
  .questions_list_item {
    margin-bottom: 1.5rem;
  }
  .questions_list_item.error {
    color: #ff0000;
  }
  .question_title {
    padding: 0.5rem;
    background-color: #f4f4f4;
    border-left: 4px solid var(--secondary-color);
  }
  .question_options {
    margin: 0.5rem 0;
  }
  .custom-control-input:checked ~ .custom-control-label::before {
    background-color: var(--primary-color);
    border-color: var(--primary-color);
  }
  .questions_button_wrapper {
    text-align: center;
    margin: 2rem 0 1rem;
  }
  .questions_buttons {
    border-color: var(--primary-color);
    background-color: var(--primary-color);
  }
</style>
