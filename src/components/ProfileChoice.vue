<template>
  <div class="ProfileChoice">
    <div v-if="!match[0]?.name">
      Lade Daten...
    </div>
    <div class="left">
      <canvas id="radar"></canvas>
      <!-- <button class="button">Neustart</button> -->
    </div>
    <div class="right" v-if="match[0]?.name">
      <h2>{{ match[0].name }}</h2>
      <p v-html="match[0].taste"></p>
      <p><b>Weinfarbe:</b><br/>
        {{ match[0].color }}
      </p>
      <p><b>Aromen:</b><br/>
        {{ match[0].aroma }}
      </p>
      <div class="buttons">
        <button
            v-for="answer in answers"
            class="button"
            :key="answer.id"
            @click="this.$emit('answerClicked', answer.id)"
        >{{ answer.text }}
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {Chart, ChartItem, registerables} from "chart.js";
import {MatchType} from "@/interfaces/MatchType";
import {AnswerType} from "@/interfaces/AnswerType";

let colors = [
  {
    backgroundColor: 'rgba(255, 99, 132, 0.2)',
    borderColor: 'rgb(255, 99, 132)',
  },
  {
    backgroundColor: 'rgba(54, 162, 235, 0.2)',
    borderColor: 'rgb(54, 162, 235)',
  },
  {
    backgroundColor: 'rgba(235,211,54,0.2)',
    borderColor: 'rgb(235,217,54)',
  },
  {
    backgroundColor: 'rgba(54,235,99,0.2)',
    borderColor: 'rgb(87,235,54)',
  },
]

export default defineComponent({
  name: 'ProfileChoice',
  emits: ['answerClicked'],
  props: {
    matches: {
      type: Object as PropType<MatchType[]>
    },
    answers: {
      type: Object as PropType<AnswerType[]>
    }
  },
  created() {
    Chart.register(...registerables)
  },
  data() {
    return {
      match: [
        ({'name': '', 'points': [0,0,0,0,0]} as MatchType)
      ]
    }
  },
  mounted(){
    this.match = this.matches as MatchType[];

    let ctx = document.getElementById('radar') as ChartItem

    new Chart(ctx, {
      type: 'radar',
      data: {
        labels: ['Süße', 'Säure', 'Alkohol', 'Körper', 'Fruchtigkeit'],
        datasets: [
          {
            label: 'Dein Geschmacksprofil',
            data: (this.matches as MatchType[])[0].points,
            backgroundColor: colors[0].backgroundColor,
            borderColor: colors[0].borderColor
          }
        ]
      },
      options: {
        responsive: false,
        scales: {
          r: {
            angleLines: {
              display: true
            },
            min: 0,
            max: 5
          }
        }
      }
    })
  },
  watch: {
    matches: function(newVal: MatchType[]) { // watch it
      console.log("Watch matches");
      console.log(newVal);
      this.match = newVal;

      let ctx = document.getElementById('radar') as ChartItem

      new Chart(ctx, {
        type: 'radar',
        data: {
          labels: ['Süße', 'Säure', 'Alkohol', 'Körper', 'Fruchtigkeit'],
          datasets: [
            {
              label: 'Dein Geschmacksprofil',
              data: newVal[0].points,
              backgroundColor: colors[0].backgroundColor,
              borderColor: colors[0].borderColor
            }
          ]
        },
        options: {
          responsive: false,
          scales: {
            r: {
              angleLines: {
                display: true
              },
              min: 0,
              max: 5
            }
          }
        }
      })
    }
  }
});
</script>

<style scoped lang="scss">
.ProfileChoice {
  flex-direction: row;
  flex-flow: row nowrap;
  justify-content: space-between;
  display: flex;
  margin-bottom: 50px;
  margin-top: 20px;
}

.button {
  cursor: pointer;
  background-color: #f67e7d;
  margin: 30px auto 0 auto;
  border: none;
  color: #fff;
  border-radius: 30px;
  max-width: 225px;
  padding: 13px 35px 15px;
  text-transform: uppercase;

  &:hover {
    background-color: #fa6261;
  }
}

.right, .left {
  display: flex;
  flex-direction: column;
  flex-flow: column;
}

.right {
  text-align: left;
  margin-left: 20px;
  margin-top: 20px;
}

.left{
  @media only screen and (max-width: 900px) {
    display:none;
  }

  .button{
    background-color: transparent;
    color: #631841;
    border: 1px solid #631841;
  }
}

.buttons {
  display: flex;
  flex-direction: row;
  flex-flow: row nowrap;
  justify-content: space-between;
}


</style>
