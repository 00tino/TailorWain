<template>
  <div class="progressbar">
    <span class="progress" :style="{width: Math.floor((progress-1)/overall*100) + '%'}"></span>
  </div>
  <span class="prozent">{{ Math.floor((progress-1)/overall*100) }} %</span>
</template>

<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
  name: 'Header',
  props: ['progress', 'overall']
});
</script>

<style scoped>
  .progressbar{
    width: 100%;
    height: 10px;
    background-color: #f67e7d;
    position: relative;
    box-shadow: rgba(0, 0, 0, 0.18) 0px 1px 1px;
    margin-bottom: 5px;
	
  }

  .progress {
    background-color: #743C61;
    height: 10px;
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    transition: .3s;
  }
  
   .prozent {
	color: #743C61;
    font-size: 14px;
    background-color: #ebe8e1;
  }

  
  
 
</style>
