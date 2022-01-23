<template>
  <div class="intro">
    <h2>Wein ist einfach <span style="text-decoration: line-through">zu kompliziert!</span></h2>
    <p class="slogan">Einfach, Individuell, Schnell</p>

    <p class="second">Mit ein paar Klicks zum persönlichen Lieblingswein:</p>
    <ol>
      <li>Wir ermitteln dein <span class="underline">persönliches Geschmacksprofil.</span></li>
      <li>Wir verraten dir, welcher Wein zu dir passt.</li>
      <li>Wähle dein Essen aus, zu dem dein Wein passen soll.</li>
      <li>Dein <span class="underline">Essen & Lieblingswein</span> auf einen Blick.</li>
    </ol>

    <div class="StartChoice">
      <button class="button"
          v-for="answer in answers"
          :key="answer.id"
          @click="this.$emit('answerClicked', answer.id)"
      >Mache das Quiz
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {AnswerType} from "@/interfaces/AnswerType";

export default defineComponent({
  name: 'StartChoice',
  emits: ['answerClicked'],
  props: {
    answers: {
      type: Object as PropType<AnswerType[]>
    }
  }
});
</script>

<style scoped lang="scss">
  .intro {
    width: 550px;
    text-align: center;
    margin: 0 auto;

    h2 {
      margin: 0;
      font-size: 25px;
      font-weight: 500;
    }

    ol {
      max-width: 500px;
      counter-reset: my-awesome-counter;
      list-style: none;
      padding-left: 80px;
      text-align: left;
    }
    ol li {
      counter-increment: my-awesome-counter;
      position: relative;
      margin: 20px 0;
      font-size: 19px;
    }
    ol li::before {
      content: counter(my-awesome-counter);
      color: white;
      font-size: 15px;
      position: absolute;
      width: 24px;
      height: 24px;
      line-height: 22px;
      font-weight: bold;
      left: -34px;
      top: 0;
      background-color: #631841;
      border-radius: 50%;
      text-align: center;
    }

    .underline{
      display: inline-block;
    }

    .underline::before{
      content: " ";
      border: solid 3px #f67e7d;
      display: block;
      margin-bottom: -50px;
      border-color: #f67e7d transparent transparent transparent;
      border-radius: 50%/8px 2px 0 0;
      height: 21px;
    }

    .slogan {
      font-weight: 400;
      text-transform: uppercase;
      margin: 0 0 30px 0;
      font-size: 16px;
    }

    p {
      font-size: 20px;
    }
	



  }


.StartChoice {
  flex-direction: column;
  flex-flow: row wrap;
  justify-content: space-around;
  display: flex;
}

  .button{
    cursor: pointer;
    background-color: #f67e7d;
    margin: 30px auto 0 auto;
    border: none;
    color: #fff;
    border-radius: 30px;
    max-width: 225px;
    padding: 13px 35px 15px;
    text-transform: uppercase;

    &:hover{
      background-color: #fa6261;
    }
  }
</style>
