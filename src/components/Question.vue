/*
Here we got the question text, images and the answers
*/

<template v-if="question">
  <!--<span class="headline">{{ question.headline }}</span> -->
  <span class="text">{{ question.text }}</span>

  <div v-if="displayFrame(question.questionType) && question.picture && assetPath" class="frame"
       :style="{backgroundImage: 'url(' + assetPath + 'frame.png)' }">
    <img :src="assetPath + question.picture" :alt="question.text"/>
    <div class="explanation">{{ question.explanation }}</div>
  </div>
  <div v-else>
    <span class="explanation">{{ question.explanation }}</span>
    <div v-if="question.picture && assetPath" class="picture">
      <img :src="assetPath + question.picture" :alt="question.text"/>
    </div>
  </div>

  <component :is="questionType"
             @answerClicked="$emit('answerClicked', $event)"
             :answers="question.answers"
             :matches="question.matches">
  </component>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import MultipleChoice from "@/components/MultipleChoice.vue";
import MultiplePictureChoice from "@/components/MultiplePictureChoice.vue";
import BinaryChoice from "@/components/BinaryChoice.vue";
import {QuestionComponents} from "@/interfaces/QuestionComponents";
import {QuestionType} from "@/interfaces/QuestionType";
import StartChoice from "@/components/StartChoice.vue";
import SwipeChoice from "@/components/SwipeChoice.vue";
import ResultChoice from "@/components/ResultChoice.vue";
import ProfileChoice from "@/components/ProfileChoice.vue";

export default defineComponent({
  name: 'Question',
  components: {MultipleChoice, MultiplePictureChoice, BinaryChoice, StartChoice, SwipeChoice, ResultChoice, ProfileChoice},
  inject: ['assetPath'],
  emits: ['answerClicked'],
  props: {
    question: {
      type: Object as PropType<QuestionType>
    }
  },
  computed: {
    questionType(): string {
      return QuestionComponents[(this.question as QuestionType).questionType]
    }
  },
  methods: {
    displayFrame(q: QuestionComponents):boolean {
      return q == QuestionComponents.SwipeChoice
    }
  }
});
</script>

<style scoped lang="scss">
.headline {
  align-self: flex-start;

}

.text {
  font-size: 30px;
  margin-top: -5px;
  margin-bottom: 20px;
}

.explanation {
  font-size: 16px;
  margin-top: 10px;
}

.picture {
  height: 200px;
  margin: 20px 0;

  img {
    max-height: 100%;
  }
}

.frame {
  background-repeat: no-repeat;
  height: 500px;
  background-position: center;

  img{
    margin-top: 80px;
    width: 300px;
  }

  .explanation{
    margin-top: 25px;
  }
  
  
}
</style>
