/*
Yes No Buttons
*/

<template>
  <div class="BinaryChoice">
    <BinaryChoiceButton
        v-for="answer in answers"
        :answer="answer"
        :key="answer.id"
        @click="this.$emit('answerClicked', answer.id)"
    ></BinaryChoiceButton>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import BinaryChoiceButton from "@/components/BinaryChoiceButton.vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'BinaryChoice',
  components: {BinaryChoiceButton},
  emits: ['answerClicked'],
  props: {
    answers: {
      type: Object as PropType<AnswerType[]>
    }
  }
});
</script>

<style scoped>
  .BinaryChoice{
    flex-direction: column;
    flex-flow: row wrap;
 /*   justify-content: space-around; */
    display: flex;
  }
</style>
