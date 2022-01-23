/*
Yes No Buttons
*/

<template>
  <div class="SwipeChoice">
    <button
        v-for="answer in answers"
        class="button"
        :key="answer.id"
        @click="this.$emit('answerClicked', answer.id)"
    >{{answer.text}}</button>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'SwipeChoice',
  emits: ['answerClicked'],
  props: {
    answers: {
      type: Object as PropType<AnswerType[]>
    }
  }
});
</script>

<style scoped lang="scss">
  .SwipeChoice{
    flex-direction: column;
    flex-flow: row wrap;
    justify-content: space-around;
  /*  display: flex; */
    margin-bottom: 50px;
  }

  .button{
    
    cursor: pointer;
    background-color: #f67e7d;
    margin: 10px;
    border: none;
    color: #fff;
    border-radius: 30px;
    width: 100px;
	height: 50px;
	font-size: 17px;
   
    text-transform: uppercase;

    &:hover{
      background-color: #fa6261;
    }
  }
</style>
