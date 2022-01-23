/*
  Display back button
*/

<!--
<template>
 <button class="button" @click.prevent="$emit('prevQuestion')" v-if="prevVisible">Zurück</button>
</template>
-->

<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
  name: 'Navigation',
  props: {
    prevVisible: {
      type: Boolean
    }
  },
  emits: ['prevQuestion']
});
</script>

<style scoped lang="scss">
  .button{
    cursor: pointer;
    background-color: #631841;
    margin: 0 auto;
    border: none;
    color: #fff;
    border-radius: 30px;
    font-weight: bold;
    max-width: 225px;
    padding: 13px 35px 15px;
    text-transform: uppercase;

    &:hover{
      background-color: #791D4E;
    }
  }


</style>
