<template>
  <div @click="sayWord" class="clickable">
    <img src="/speak.jpg" alt="Speak" />
    <h3>Say Word</h3>
  </div>
</template>

<script>
export default {
  props: ["word"],
  methods: {
    sayWord() {
      const utterance = new SpeechSynthesisUtterance(this.word);
      speechSynthesis.speak(utterance);
    }
  },

  // Optional. See Vue watchers
  watch: {
    word() {
      this.sayWord();
    }
  }
};
</script>

<style scoped>
.clickable {
  cursor: pointer;
}
h3 {
  margin-top: -35px;
}
</style>
