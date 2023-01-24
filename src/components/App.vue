<template>
  <main>
    <div class="container">
      <h1>Frontend Quiz</h1>
      <div class="question">{{}}</div>
      <p>score is {{ score }}</p>
    </div>
  </main>
</template>

<script>
import questions from "./questions.json";
export default {
  data() {
    return {
      value: 0,
      questions: questions,
      quizCompleted: false,
      currentQuestion: 0,
    };
  },
  methods: {
    setAnswer(e) {
      this.questions[this.currentQuestion].selected = e.target.value;
    },
  },
  computed: {
    score() {
      let score = 0;
      this.questions.forEach((q) => {
        if (q.selected === q.answer) score++;
      });
      return score;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  min-height: 100vh;
  background-color: #271c36;
  font-family: "montserrat", sans-serif;
}
</style>
