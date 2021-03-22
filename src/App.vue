<template>
  <div id="app">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBottom
            v-if="result.length"
            :currentQuestion="result[index]"
            :nextQuestion="next"
            :allOptions="allOptions"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header";
import QuestionBottom from "./components/QuestionBottom";

export default {
  name: "App",
  components: {
    Header,
    QuestionBottom,
  },

  methods: {
    next() {
      this.index++;
    },
  },
  data() {
    return {
      result: [],
      index: 0,
    };
  },
  mounted: function() {
    this.axios
      .get("https://opentdb.com/api.php?amount=10")
      .then((response) => {
        return (this.result = response.data.results);
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
#app {
}
</style>
