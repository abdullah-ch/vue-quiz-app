/* eslint-disable no-unused-labels */
<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template slot="lead">
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answers, index) in allOptions"
          :key="index"
          @click="selectedAns(index)"
          :class="answerTyped(index)"
        >
          {{ answers }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
      >
        Submit
      </b-button>
      <b-button variant="success" @click="nextQuestion">
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  name: "QuestionBottom",
  props: {
    currentQuestion: Object,
    nextQuestion: Function,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      answered: false,
    };
  },
  // watch listens for changes to the props
  watch: {
    currentQuestion() {
      this.selectedIndex = null;
      this.answered = false;
    },
    allOptions() {
      this.correctIndex = this.allOptions.indexOf(
        this.currentQuestion.correct_answer
      );
      console.log("Correct index isss", this.correctIndex);
    },

    // I want this method to run when props are passed to the component
    //Currently, it only runs after the computed method has been executed
  },

  computed: {
    allOptions() {
      let allOptions = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer,
      ];
      //  console.log("array that is not shuffled is ", allOptions);
      allOptions = _.shuffle(allOptions);
      console.log("shuffled array is", allOptions);
      // console.log("Corect ans is ", this.currentQuestion.correct_answer);
      console.log("I am first");
      return allOptions;
    },
  },

  methods: {
    selectedAns(index) {
      this.selectedIndex = index;
      console.log("Selected answer index", this.selectedIndex);
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },

    answerTyped(index) {
      let className = "";

      if (this.answered && index === this.correctIndex) {
        className = "correct";
      } else if (!this.answered && index === this.selectedIndex) {
        className = "selected";
      } else if (
        this.answered &&
        index === this.selectedIndex &&
        index !== this.correctIndex
      ) {
        className = "wrong";
      }

      return className;
    },
  },

  mounted: function() {
    this.correctIndex = this.allOptions.indexOf(
      this.currentQuestion.correct_answer
    );
    console.log("Correct index isss", this.correctIndex);
  },
};
</script>

<style scoped>
.list-group-item {
  color: black;
  display: flex;
  justify-content: center;
}

.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}

.button {
  display: flex;
}
.btn {
  /* display: flex; */

  /* margin-top: 1rem;
  margin-right: 1rem; */
}

/* .btn-secondary {
  margin-left: 9rem;
} */

.correct {
  background-color: green;
}

.wrong {
  background-color: red;
}

.selected {
  background-color: lightblue;
}
</style>
