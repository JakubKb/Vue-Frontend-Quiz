<template>
  <main>
    <div class="container">
      <div class="questions">
        <div class="question-text">
          <h2 v-if="questions[0]" :key="questions[0].id">
            {{ questions[0].question }}
          </h2>
        </div>
      </div>
      <div class="answers">
        <button v-for="(option, index) in questions[0].options" :key="index">
          {{ option }}
        </button>
      </div>
    </div>
  </main>
</template>

<script>
const questions = [
  {
    id: 0,
    question: "What is OOP?",
    answer: "0",
    options: [
      "Object-oriented programming",
      "Out of place",
      "Ordinary output process",
      "Optimized operating performance",
    ],
    selected: null,
  },
  {
    id: 1,
    question: "What is the virtual DOM?",
    answer: "1",
    options: [
      "A physical representation of the HTML Document",
      "An in-memory representation of the actual DOM",
      "A way to optimize website's performance",
      "A JavaScript library for handling events",
    ],
    selected: null,
  },
  {
    id: 2,
    question:
      "What is the difference between server-side rendering and client-side rendering?",
    answer: "2",
    options: [
      "Server-side rendering is for backend and client-side rendering is for frontend",
      "Server-side rendering is faster than client-side rendering",
      "Server-side rendering renders the pages on the server, while client-side rendering renders the pages in the browser",
      "Server-side rendering is for static pages and client-side rendering is for dynamic pages",
    ],
    selected: null,
  },
];

export default {
  data() {
    return {
      questions: questions,
    };
  },
};

console.log(questions);
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
  color: white;
}
</style>
