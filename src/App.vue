<template>
    <div class="container">
      <app-quote-progress :maxQuotes="maxQuotes"></app-quote-progress>
      <app-add-quote></app-add-quote>
      <div class="quotes">
        <template v-for="(quote, index) in quotes">
          <app-quote-entity :id="index">{{quote}}</app-quote-entity>
        </template>
      </div>
    </div>
</template>

<script>
import QuoteEntity from './components/QuoteEntity.vue';
import QuoteProgress from './components/QuoteProgressBar.vue';
import AddQuote from './components/AddQuote.vue';
import { appBus } from './main';
export default {
  data() {
    return {
      quotes: [],
      maxQuotes: 10
    }
  },
  components: {
    'app-quote-progress': QuoteProgress,
    'app-quote-entity': QuoteEntity,
    'app-add-quote': AddQuote
  },
  watch: {
    quotes(value) {
      appBus.$emit('quotesNumberChanged', value.length);
    }
  },
  created() {
    appBus.$on('newQuote', (text) => {
      if (this.quotes.length < this.maxQuotes) {
        this.quotes.push(text);
        appBus.$emit('quoteAdded', true);
      } else {
        alert('Слишком много цитат! Чтобы добавить новые, удалите лишние');
      }

    });
    appBus.$on('deleteQuote', (id) => {
      this.quotes.splice(id, 1);
    });
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
  }

  .quotes {
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
  }

  .container {
    width: 90%;
    padding: 10px 0;
    margin: 20px auto;
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
  }
</style>
