<script setup>
import { ref } from 'vue';
import easy_json from '../assets/QuincasBorbas_Short_Easy.json';
import hard_json from '../assets/QuincasBorbas_Short_Hard.json';

defineProps({
  msg: String,
});

const count = ref(0);
</script>

<script>
export default {
  data() {
    return {
      list_tokens: [],
      difficulty: 'Easy',
      array: [],
      array_index: 0,
    };
  },

  created() {
    this.list_tokens = easy_json.book[this.count].text.split(' ');
    this.array = this.list_tokens.slice(
      this.array_index,
      this.array_index + 10
    );
    this.array = this.array.join(' ');
  },
  methods: {
    next_chapter() {
      this.count++;
      this.get_chapter();
      this.array_index = 1;
    },
    previous_chapter() {
      this.count--;
      this.get_chapter();
      this.array_index = 1;
    },
    get_chapter() {
      if (this.difficulty == 'Hard') {
        this.list_tokens = hard_json.book[this.count].text.split(' ');
      } else {
        this.list_tokens = easy_json.book[this.count].text.split(' ');
      }
    },
    nextList() {
      if (this.array_index < this.list_tokens.length - 9) {
        this.array_index++;
        this.array = this.list_tokens.slice(
          this.array_index,
          this.array_index + 10
        );
        this.array = this.array.join(' ');
      }
    },
  },
  computed: {
    showList() {
      return this.array;
    },
  },
};
</script>

<template>
  <h1>{{ msg }}</h1>

  <p>
    Recommended IDE setup:
    <a href="https://code.visualstudio.com/" target="_blank">VS Code</a>
    +
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
  </p>

  <p>
    <a href="https://vitejs.dev/guide/features.html" target="_blank">
      Vite Documentation
    </a>
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Documentation</a>
  </p>

  <button type="button" @click="next_chapter">Next Chapter {{ count }}</button>
  <p>{{ hard_json.book.title }}</p>
  <p>{{ hard_json.book[count].chapter }}</p>
  <p>Dificuldade {{ difficulty }}</p>
  <p>Texto Completo: {{ list_tokens.join(' ') }}</p>
  <button type="button" @click="nextList">Next List</button>
  <p>{{ showList }}</p>
  <p>Indice {{ array_index }}</p>
  <button type="button" @click="previous_chapter">Previous Chapter</button>
  <!--TODO: Check last chapter-->
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
