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
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answers }}
        </b-list-group-item>
      </b-list-group>

      <b-button @click="submitAnswer">
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
      shuffleArray: [],
      ansArray: [],
    };
  },
  // watch listens for changes to the props
  watch: {
    currentQuestion() {
      this.selectedIndex = null;
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
      this.increment(isCorrect);
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

.btn {
  justify-content: center;
  margin-top: 1rem;
  margin-right: 1rem;
}

.btn-secondary {
  margin-left: 9rem;
}

.correct {
  color: green;
}

.wrong {
  color: red;
}

.selected {
  background-color: lightblue;
}
</style>
