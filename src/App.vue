<template>
  <div id="app">
    <h1>Spelling Test</h1>
    <div v-if="!testFinished">
      <p>Word {{ activeIndex + 1 }} of {{ questions.length }}</p>
      <speech :word="questions[activeIndex].word" />
      <form @submit.prevent="handleSubmit">
        <input
          type="text"
          v-model="userInput"
          spellcheck="false"
          placeholder="Spell the word"
        />
        <button type="submit">SUBMIT</button>
      </form>
    </div>
    <div v-else>
      <score :data="questions" />
    </div>
  </div>
</template>

<script>
import data from "./data";
import Speech from "./components/Speech";
import Score from "./components/Score";

export default {
  components: { Speech, Score },

  data() {
    return {
      questions: data,
      activeIndex: 0,
      userInput: ""
    };
  },
  methods: {
    handleSubmit() {
      this.questions[this.activeIndex].userInput = this.userInput;
      this.activeIndex += 1;
      this.userInput = "";
    }
  },
  computed: {
    testFinished() {
      return this.questions.every(q => q.userInput);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input {
  color: #333;
  font-size: 2.5rem;
  margin: 0 auto;
  padding: 1.5rem 2rem;
  border: 4px solid black;
  border-radius: 0.2rem;
  width: 40%;
  display: block;
  margin-bottom: 20px;
  text-align: center;
}

button {
  display: inline-block;
  padding: 0.6em 1.2em;
  border: 0.1em solid black;
  margin: 0 0.3em 0.3em 0;
  border-radius: 0.2rem;
  box-sizing: border-box;
  text-decoration: none;
  text-align: center;
  transition: all 0.4 s;
  font-size: 1.5rem;
  cursor: pointer;
}
button:hover {
  color: white;
  background-color: black;
}
</style>
