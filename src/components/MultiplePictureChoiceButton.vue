<template>
  <div class="MultiplePictureChoiceButton" :class="{selected: answer.selected}" :title="answer.text">
    <span class="tooltip">{{ answer.text }}</span>
    <div class="button">
      <div class="picture">
        <img v-if="assetPath" :src="assetPath + answer.picture" :alt="answer.text"/>
      </div>
    </div>
    <div v-if="showCaption" class="caption">{{ answer.text }}</div>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'MultiplePictureChoiceButton',
  props: {
    answer: {
      type: Object as PropType<AnswerType>
    },
    showCaption: {
      type: Boolean
    }
  },
  inject: ['assetPath'],
});
</script>

<style scoped lang="scss">
  .MultiplePictureChoiceButton {
    cursor: pointer;
    margin: 10px 0;

    &:hover{
      .button {
        border-radius: 50px 80px;
        opacity: 1;
      }

      .tooltip{
        opacity: 1;
      }

      .caption {
        border-top-color: gray;
        border-bottom-color: gray;
      }
    }

    &.selected{
      .button {
       border-color: #152545;
      }
    }
  }

  .button{
    border-radius: 40px;
    border: 4px solid #F5F5F5;
    margin: 0px 10px 0px 0px;
    opacity: 0.75;
    padding: 5px 5px;
    transition: .3s;

  }

  .picture{
    height: 240px;
    width: 240px;

    img{
      max-width: 100%;
    }
  }

  .tooltip {
    opacity: 0;
    transition: .5s;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.25) 0px 2px 3.84px;
    color: #666;
    padding: 5px 25px;
  }

  .caption {
  margin-top: 10px;
     
    margin-right: 20px;
    margin-left: 20px;
 
    padding: 10px 0;
    border-top: 1px solid white;
    border-bottom: 1px solid white;
	
    transition: .3s;
    font-size: 18px;
  }
</style>
