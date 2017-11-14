<template>
    <div class="add-quote">
      <h3 class="add-quote__title">Цитата:</h3>
      <textarea rows="5" v-model="quoteValue"></textarea>
      <button class="btn" @click="addQuote">Добавить</button>
    </div>
</template>

<script>
  import { appBus } from '../main';
export default {
  data() {
    return {
      quoteValue: ''
    }
  },
  methods: {
    addQuote() {
      if (this.quoteValue.length > 0) {
        appBus.$emit('newQuote', this.quoteValue);
      }
    }
  },
  created() {
    appBus.$on('quoteAdded', (bool) => {
      if (bool) {
        this.quoteValue = '';
      }
    });
  }
}
</script>

<style scoped>
  .add-quote {
    width: 80%;
    text-align: center;
  }
  textarea {
    display: block;
    width: 80%;
    margin: 20px auto;
    padding: 20px;
    outline: none;
    border-radius: 5px;
    resize: none;
    overflow: hidden;
  }
  .btn {
    cursor: pointer;
    padding: 10px 20px;
    color: white;
    background-color: #5fa4ff;
    border: none;
    border-radius: 5px;
    outline: none;
    box-shadow: 1px 1px 2px grey;
  }
  .btn:active {
    background-color: #1aa3ff;
  }
</style>
