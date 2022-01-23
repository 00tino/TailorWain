/*
Multiple Choice with text answers
*/

<template>
  <div class="MultipleChoice">
    <MultipleChoiceButton
        v-for="answer in answers"
        :key="answer.id"
        :answer="answer"
        @click="this.$emit('answerClicked', answer.id)">
    </MultipleChoiceButton>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import MultipleChoiceButton from "@/components/MultipleChoiceButton.vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'MultipleChoice',
  emits: ['answerClicked'],
  components: {MultipleChoiceButton},
  props: {
    answers: {
      type: Object as PropType<AnswerType[]>
    }
  }
});
</script>

<style scoped>
.MultipleChoice {
  flex-direction: column;
  flex-flow: row wrap;
  display: flex;
  margin: 20px 0;
  justify-content: space-around;
}

</style>
