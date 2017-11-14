<template>
    <blockquote class="quote" @click="deleteQuote">
      <slot></slot>
    </blockquote>
</template>

<script>
  import { appBus } from '../main.js';
export default {
  props: ['id'],
  methods: {
    deleteQuote() {
      appBus.$emit('deleteQuote', this.id);
    }
  }
}
</script>

<style scoped>
  @keyframes aboutToDelete {
    from {
      background-color: rgba(255, 100, 105, 0.24);
      color: rgba(0, 0, 0, 0.23);
    }
    to {
      background-color: rgba(255, 87, 77, 0.71);
    }
  }
  .quote {
    cursor: pointer;
    min-height: 50px;
    min-width: 200px;
    border: 1px solid grey;
    box-shadow: 1px 1px 2px rgba(128, 128, 128, 0.45);
    border-radius: 5px;
    padding: 20px 15px;
    font-family: Caveat, serif;
    font-size: 24px;
  }
  .quote:hover {
    animation-name: aboutToDelete;
    animation-duration: 0.4s;
    animation-direction: alternate;
    animation-iteration-count: infinite;
  }
</style>
