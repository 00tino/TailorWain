<template>
  <div class="MultipleChoiceButton" :class="{selected: answer.selected}" :title="answer.text">
    <div class="circle">
      <div class="checkmark"><span v-if="answer.selected">●</span></div>
    </div>
    <span class="text">{{answer.text}}</span>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'MultipleChoiceButton',
  props: {
    answer: {
      type: Object as PropType<AnswerType>
    }
  }
});
</script>

<style scoped lang="scss">

.MultipleChoiceButton {
  cursor: pointer;
  width: 75%;
  border: 2px solid grey;
  box-sizing: border-box;
  display: flex;
  transition: .3s;
  border-radius: 5px;
  margin-bottom: 10px;

  &:hover{
    border-color: #152545;

    .text{
      color: rgba(0,0,0,1);
    }
   }
}

.circle {
  margin-left: 10px;
  height: 18px;
  border-radius: 20px;
  border-width: 2px;
  border-style: solid;
  border-color: #743C61;
  top: 30%;
  position: relative;
}
.checkmark {
  width: 18px;
  font-weight: 500;
  font-size: 26px;
  color: #743C61;
  position: relative;
  top: -12px;
}

.text{
  padding: 12px 10px;
  margin-left: 10px;
  color: rgba(0,0,0,0.65);
  transition: .3s;
  font-size: 20px;
}

</style>
