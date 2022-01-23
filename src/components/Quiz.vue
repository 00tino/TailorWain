// @ts-nocheck

/*
Here the Quiz is displayed, containing the header, question and footer
*/

<template>
  <img :src="assetPath + '/header.png'" class="frame" />
  <div class="tt_wrapper">
    <Header v-if="currentQuestion.position" :progress="currentQuestion.position" :overall="lastPosition-1"></Header>
    <div class="question">
      <Question :question="currentQuestion" @answerClicked="setAnswer"></Question>
    </div>
    <Navigation @prevQuestion="prevQuestion" :prev-visible="currentQuestion.position > 1"></Navigation>
    <a class="refLink" href="https://wein.today/" target="_blank">powered by Tailorwine</a>
  </div>
  <img :src="assetPath + '/footer.png'" class="frame" />
</template>

<script lang="ts">
import Header from './Header.vue';
import Navigation from './Navigation.vue';
import Question from './Question.vue';
import QuizService from "@/services/QuizService";
import {defineComponent, provide, ref} from "vue";
import {QuestionType} from "@/interfaces/QuestionType";
import {QuizType} from "@/interfaces/QuizType";
import {AnswerType} from "@/interfaces/AnswerType";
import ApiService from "@/services/ApiService";
import {QuizDataType} from "@/interfaces/QuizDataType";
import {QuestionComponents} from "@/interfaces/QuestionComponents";

export default defineComponent({
  name: 'Quiz',
  props: ['assetPath', 'apiEndpoint', 'shopUrl'],
  components: {Question, Navigation, Header},
  data() {
    return {
      questionHistory: [] as number[],
      quizData: {} as QuizType,
    }
  },
  setup() {
    const assetPathRef = ref(null);
    provide('assetPath', assetPathRef);
    return {
      assetPathRef
    }
  },
  beforeMount() {
    this.quizData = QuizService.getQuiz(1);
    this.questionHistory.push(this.getFirstQuestionId());
  },
  beforeUpdate() {
    ApiService.setEndpoint(this.apiEndpoint);
    this.assetPathRef = this.assetPath;
  },
  computed: {
    lastPosition(): number {
      return this.quizData.questions.reduce((prev: QuestionType, current: QuestionType) =>
          (prev.position > current.position) ? prev : current).position;
    },
    currentQuestion(): QuestionType {
      return this.getQuestionById(this.questionHistory[this.questionHistory.length - 1]);
    }
  },
  methods: {
    setAnswer(answerId: number): void {
      // Set answer
      this.currentQuestion.answers.forEach((answer) => {
        answer.selected = answer.id === answerId;
      });
      let answer = this.getAnswerById(answerId);
      let answers: QuizDataType[] = []



      // If next question just send current answer
      if (answer.nextQuestion) {
        // eslint-disable-next-line
        window.setTimeout(function (this: any) {
          this.questionHistory.push(this.getQuestionById(answer.nextQuestion).id);
          document.getElementsByClassName('tt_wrapper')[0].scrollIntoView(
              {behavior: "smooth", block: "start", inline: "nearest"}
          );
        }.bind(this), 250);
      }

      for (const questionId of this.questionHistory) {
        let selectedAnswer = (this.getQuestionById(questionId).answers.find((ele) => {
          return ele.selected
        }) as AnswerType)

        answers.push({
          'answerId': selectedAnswer.id,
          'score': selectedAnswer.score,
          'questionId': questionId
        })
      }
      answers.push({'questionId': this.currentQuestion.id, 'answerId': answer.id, 'score': answer.score})

      let nextQuestion = this.getQuestionById(answer.nextQuestion as number)
      if( nextQuestion.questionType === QuestionComponents.ResultChoice ||
          nextQuestion.questionType === QuestionComponents.ProfileChoice) {

        // Do API call
        let promise = QuizService.getMatch(answers)
        promise.then((responseJson) => {
          nextQuestion.matches = responseJson.matches;
        })
      }
    },
    prevQuestion(): void {
      this.questionHistory.pop();
    },
    getQuestionById(questionId: number): QuestionType {
      return this.quizData.questions.find((ele) => {
        return ele.id === questionId
      }) as QuestionType;
    },
    getAnswerById(answerId: number): AnswerType {
      return this.currentQuestion.answers.find((ele) => {
        return ele.id === answerId
      }) as AnswerType;
    },
    getFirstQuestionId(): number {
      return (this.quizData.questions.find((ele) => {
        return ele.position === 0
      }) as QuestionType).id;
    }
  }
});
</script>

<style scoped lang="scss">

.tt_wrapper, .question {
  display: flex;
  flex-direction: column;
  transition: .3s;
}

.tt_wrapper {
  display: flex;
  width: 60%;
  margin: 0 auto;
}

.question {
  width: 100%;
  align-self: center;
}

.refLink {
  text-decoration: none;
  color: lightgray;
  margin: 20px auto 0 auto;

  &:hover {
    color: grey;
  }
}

.frame {
  width: 100%;
  height: auto;
  display: block;
}
</style>
