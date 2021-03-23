<template>
  <div>
    <div>
      <b-nav tabs>
        <b-nav-item disabled>Sombe Quiz App</b-nav-item>
        <b-nav-item disabled
          >Counter: {{ correctAnswer }}/{{ totalQuestions }}</b-nav-item
        >
      </b-nav>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",

  props: {
    correctAnswer: Number,
    totalQuestions: Number,
  },
};
</script>
