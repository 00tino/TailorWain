<template>
  <Quiz :asset-path="assetPath" :api-endpoint="apiEndpoint" :shop-url="shopUrl"/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Quiz from "@/components/Quiz.vue";

export default defineComponent({
  name: 'App',
  data() {
    return {
      'assetPath': '',
      'apiEndpoint': '',
      'shopUrl': '',
    }
  },
  mounted() {
    this.assetPath = this.$el.parentNode.dataset.assetPath;
    this.apiEndpoint = this.$el.parentNode.dataset.apiEndpoint;
    this.shopUrl = this.$el.parentNode.dataset.shopUrl;
  },
  components: {
    Quiz
  }
});
</script>

<style lang="scss">
#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
  font-size: 14px;
  background-color: #ebe8e1;
}
</style>
