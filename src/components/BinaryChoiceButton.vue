<template>
  <div class="BinaryChoiceButton" :class="{selected: answer.selected}" :title="answer.text">
    <img v-if="assetPath" :src="assetPath + answer.picture" :alt="answer.text"/>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'BinaryChoiceButton',
  props: {
    answer: {
      type: Object as PropType<AnswerType>
    }
  },
  inject: ['assetPath']
});
</script>

<style scoped lang="scss">
.BinaryChoiceButton {
  cursor: pointer;

  &.selected img{
    filter: grayscale(0.4);
  }

  img {
    width: 150px;
    filter: grayscale(100);
    transition: .3s;
	margin: 0px -260px 0px 260px;

    &:hover {
      filter: grayscale(0);
    }
  }
}
</style>
