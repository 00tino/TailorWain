/*
  Multiple Choice with images as answers
*/

<template>
  <div class="MultiplePictureChoice">
    <MultiplePictureChoiceButton
        v-for="answer in answers"
        :key="answer.id"
        :answer="answer"
        :show-caption="answers.length > 2"
        @click="this.$emit('answerClicked', answer.id)">
    </MultiplePictureChoiceButton>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import MultiplePictureChoiceButton from "@/components/MultiplePictureChoiceButton.vue"
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'MultiplePictureChoice',
  emits: ['answerClicked'],
  components: { MultiplePictureChoiceButton },
  props: {
    answers: {
      type: Object as PropType<AnswerType[]>
    }
  }
});
</script>

<style scoped>
  .MultiplePictureChoice {
    flex-direction: column;
    flex-flow: row wrap;
    display: flex;
    margin: 20px 0;
	align-self: center;

	
  }
</style>
