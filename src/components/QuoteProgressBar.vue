<template>
    <div class="progress">
      <h1 class="progress__title">Добавлено цитат</h1>
      <div class="progress__bar-container">
        <div class="progress__bar" :style="progressBarWidth">
          <div class="progress__value" v-if="barWidth">{{barWidth}} / {{maxQuotes}}</div>
        </div>
      </div>
    </div>
</template>

<script>
import { appBus } from '../main.js';
export default {
  props: {
    'maxQuotes': {
      type: Number,
      default: 10
    }
  },
  data() {
    return {
      barWidth: 0
    }
  },
  created() {
    appBus.$on('quotesNumberChanged', (value) => {
      this.barWidth = value;
    });
  },
  computed: {
    progressBarWidth() {
      return {
        width: `${this.barWidth * 10}%`
      }
    }
  }
}
</script>

<style scoped>
  .progress {
    width: 100%;
    margin-bottom: 20px;
  }
  .progress__title {
    text-align: left;
  }
  .progress__bar-container {
    height: 20px;
    width: 100%;
    border: 1px solid rgba(128, 128, 128, 0.6);
    border-radius: 5px;
  }
  .progress__bar {
    position: relative;
    height: 100%;
    background-color: #5fa4ff;
    transition-duration: 0.3s;
  }
  .progress__value {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    text-align: center;
    color: white;
    overflow: hidden;
  }
</style>
