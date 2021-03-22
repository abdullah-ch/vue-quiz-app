<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template slot="lead">
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item v-for="(answers, index) in allOptions" :key="index">
          {{ answers }}
        </b-list-group-item>
      </b-list-group>

      <b-button>
        Submit
      </b-button>
      <b-button variant="success" @click="nextQuestion">
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBottom",
  props: {
    currentQuestion: Object,
    nextQuestion: Function,
  },
  computed: {
    allOptions() {
      let allOptions = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      console.log("the total options are", allOptions);
      return allOptions;
    },
  },

  mounted() {
    console.log(this.currentQuestion);
  },
};
</script>
