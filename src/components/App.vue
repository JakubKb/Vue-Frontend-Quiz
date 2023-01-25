<template>
  <main>
    <div class="container">
      <h2>Frontend quiz</h2>
      <div class="questions">
        <div class="question-text">
          <h1 v-if="questions[0]" :key="questions[0].id">
            {{ questions[0].question }}
          </h1>
          <p>Score: {{ score }}</p>
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
      score: 0,
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
  text-align: center;
}

.container {
  background-color: #1c1b1b;
  max-width: 550px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
  margin: 100px auto;
  padding: 10px;
}

h1 {
  margin-bottom: 10px;
}

h2 {
  margin-bottom: 10px;
}

button {
  font-family: inherit;
  padding: 5px 10px;
  max-width: 250px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  border-radius: 10px;
  margin-right: 10px;
  background-color: rgb(10, 145, 255);
  color: white;
  cursor: pointer;
  font-size: 17px;
}

button:hover {
  opacity: 0.7;
  transition: all ease-in-out 0.3s;
}
.answers {
  font-family: inherit;
  padding: 10px 20px;

  display: grid;
  grid-template-rows: repeat(2, 1fr);
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 10px;
}
</style>
