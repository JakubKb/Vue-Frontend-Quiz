<template>
  <main>
    <div
      class="container"
      id="container"
      :style="{ display: displayContainer }"
    >
      <h2>Frontend quiz</h2>
      <div class="questions">
        <div class="question-text">
          <h1
            v-if="questions[currentQuestionIndex]"
            :key="questions[currentQuestionIndex].id"
          >
            {{ questions[currentQuestionIndex].question }}
          </h1>

          <p>Score: {{ score }}</p>
        </div>
      </div>
      <div class="answers">
        <button
          :ref="'button' + index"
          class="answer-btn"
          :disabled="buttonsDisabled"
          v-for="(option, index) in (
            questions[currentQuestionIndex] || { options: [] }
          ).options"
          :key="index"
          @click="validateAnswer(index)"
        >
          {{ option }}
        </button>
      </div>
    </div>
    <div
      class="completed"
      id="completed"
      :style="{ display: displayCompleted }"
    >
      <h2>Quiz Completed!</h2>
      <div class="completed-text">
        <p>Your score is {{ score }} out of {{ questions.length }}</p>
      </div>
      <button class="reset" @click="reset">Reset Quiz</button>
    </div>
    <div class="preQuiz" id="preQuiz" :style="{ display: displayPreQ }">
      <h2>Frontend Quiz!</h2>
      <p>In this quiz you'll be answering frontend questions!</p>
      <br />
      <p>This is a beta version. still in development</p>
      <br />
      <a href="https://github.com/JustKooba/Vue-Frontend-Quiz">Github Repo</a>
      <button class="startQ" @click="startQuiz">3</button>
      <button class="startQ" @click="startQuiz">5</button>
      <button class="startQ" @click="startQuiz">10</button>
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
  {
    id: 3,
    question: "What is the purpose of the BEM methodology?",
    answer: "3",
    options: [
      "To create responsive designs",
      "To improve website's SEO",
      "To simplify the debugging process",
      "To improve the maintainability and scalability of the code",
    ],
    selected: null,
  },
  {
    id: 4,
    question: "What is the difference between webpack and gulp?",
    answer: "0",
    options: [
      "Webpack is a module bundler, while gulp is a task runner",
      "Webpack is for frontend development, while gulp is for backend development",
      "Webpack is for React, while gulp is for Angular",
      "Webpack is a new technology, while gulp is an old one",
    ],
    selected: null,
  },
  {
    id: 5,
    question: "What is the difference between state and props?",
    answer: "1",
    options: [
      "State is for components, while props is for elements",
      "State is for internal component's data, while props is for data passed from the parent component",
      "State is for handling events, while props is for handling data",
      "State is for handling data, while props is for handling events",
    ],
    selected: null,
  },
  {
    id: 6,
    question: "What is the difference between Redux and MobX?",
    answer: "2",
    options: [
      "Redux is for React, while MobX is for Angular",
      "Redux is for state management, while MobX is for event management",
      "Redux uses a centralized store, while MobX uses a decentralized store",
      "Redux is for managing global state, while MobX is for managing local state",
    ],
    selected: null,
  },
  {
    id: 7,
    question: "What are the benefits of using a CSS preprocessor?",
    answer: "0",
    options: [
      "It allows for the use of variables, functions, and nesting, which can improve code maintainability and reusability",
      "It improves website's performance",
      "It allows for the use of JavaScript in CSS",
      "It makes the design process faster",
    ],
    selected: null,
  },
  {
    id: 8,
    question: "What is the difference between a closure and a scope?",
    answer: "1",
    options: [
      "Closure is a function, while scope is a variable",
      "Closure is a function that has access to variables in its lexical scope, while scope refers to the accessibility or visibility of variables and functions in certain parts of the code",
      "Closure is a way to create private variables, while scope is a way to create public variables",
      "Closure is only used in JavaScript, while scope is used in all programming languages",
    ],
    selected: null,
  },
];
questions.forEach((question) => {
  question.options.sort(() => Math.random() - 0.5);
});
export default {
  data() {
    return {
      questions: questions,
      score: 0,
      currentQuestionIndex: 0,
      maxQuestionIndex: 0,
      displayContainer: "none",
      displayPreQ: "flex",
      displayCompleted: "none",
      buttonsDisabled: false,
    };
  },
  methods: {
    validateAnswer(index) {
      this.buttonsDisabled = true;
      console.log(index);
      let buttons = document.querySelectorAll(".answer-btn");
      buttons.forEach((button) => {
        button.classList.remove("incorrect");
      });

      if (index == this.questions[this.currentQuestionIndex].answer) {
        this.score++;
        this.$refs["button" + index][0].classList.add("correct");
        setTimeout(() => {
          buttons.forEach((button) => {
            button.classList.remove("correct");
          });
          this.currentQuestionIndex++;
          this.buttonsDisabled = false;
        }, 3000);
      } else {
        this.$refs["button" + index][0].classList.add("incorrect");
        setTimeout(() => {
          buttons.forEach((button) => {
            button.classList.remove("incorrect");
          });
          this.currentQuestionIndex++;
          this.buttonsDisabled = false;
        }, 3000);
      }
      if (this.currentQuestionIndex === this.maxQuestionIndex) {
        setTimeout(() => {
          this.$nextTick(() => {
            this.displayContainer = "none";
            this.displayCompleted = "flex";
            this.buttonsDisabled = false;
          });
        }, 3000);
      }
    },
    reset() {
      this.score = 0;
      this.currentQuestionIndex = 0;
      this.displayContainer = "flex";
      this.displayCompleted = "none";
    },
    startQuiz(event) {
      let buttonValue = event.target.innerText;
      if (buttonValue === "3") {
        this.maxQuestionIndex = 2;
        this.displayContainer = "flex";
        this.displayPreQ = "none";
      } else if (buttonValue === "5") {
        this.maxQuestionIndex = 4;
        this.displayContainer = "flex";
        this.displayPreQ = "none";
      } else if (buttonValue === "10") {
        this.maxQuestionIndex = 9;
        this.displayContainer = "flex";
        this.displayPreQ = "none";
      }
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
  color: white;
  text-align: center;
}
.container,
#completed,
.preQuiz {
  background-color: #1c1b1b;
  max-width: 550px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
  margin: 100px auto;
  padding: 10px;
}
.preQuiz {
  display: flex;
  text-align: center;
}
.preQuiz a {
  margin-bottom: 10px;
  text-align: center;
  margin-right: 7px;
  color: rgb(10, 145, 255);
}
.container {
  display: none;
}
#completed button {
  margin-top: 10px;
}

.startQ {
  margin-bottom: 10px;
  width: 100px;
}

#completed {
  display: none;
  justify-content: center;
  align-items: center;
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
.correct {
  background-color: rgb(10, 255, 71);
  color: white;
}
.incorrect {
  background-color: rgb(255, 71, 10);
  color: white;
}
</style>



