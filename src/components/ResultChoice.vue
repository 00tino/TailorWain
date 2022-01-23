<template>
  <div class="ResultChoice">
    <div class="left">
      <canvas id="radar"></canvas>
      <button class="button">Neustart</button>
    </div>
    <div class="right">
      <WineComponent :wine="wines[1]"></WineComponent>
      <WineComponent :wine="wines[2]"></WineComponent>
      <WineComponent :wine="wines[3]"></WineComponent>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";
import {Chart, ChartItem, registerables} from "chart.js";
import WineComponent from "@/components/WineComponent.vue";
import {MatchType} from "@/interfaces/MatchType";

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

let wines: MatchType[] = [
  {
    name: 'Lade Ergebnis...',
    points: [0,0,0,0,0]
  },
  {
    name: 'Lade Ergebnis...',
    color: '',
    taste: 100,
    aroma: 100,
    speak: '',
    points: [0,0,0,0,0]
  },
  {
    name: 'Lade Ergebnis...',
    color: '',
    taste: 50,
    aroma: 50,
    speak: '',
    points: [0,0,0,0,0]
  },
  {
    name: 'Lade Ergebnis...',
    color: '',
    taste: 25,
    aroma: 25,
    speak: '',
    points: [0,0,0,0,0]
  }
]

export default defineComponent({
  name: 'ResultChoice',
  emits: ['answerClicked'],
  components: {WineComponent},
  props: {
    matches: {
      type: Object as PropType<MatchType[]>
    }
  },
  created() {
    Chart.register(...registerables)
  },
  data() {
    return {
      wines: wines
    }
  },
  mounted(){
    this.wines = this.matches as MatchType[]

    let ctx = document.getElementById('radar') as ChartItem

    new Chart(ctx, {
      type: 'radar',
      data: {
        labels: ['Süße', 'Säure', 'Alkohol', 'Körper', 'Fruchtigkeit'],
        datasets: [
          {
            label: (this.matches as MatchType[])[0].name,
            data: (this.matches as MatchType[])[0].points,
            backgroundColor: colors[0].backgroundColor,
            borderColor: colors[0].borderColor
          },
          {
            label: (this.matches as MatchType[])[1].name,
            data: (this.matches as MatchType[])[1].points,
            backgroundColor: colors[1].backgroundColor,
            borderColor: colors[1].borderColor
          },
          {
            label: (this.matches as MatchType[])[2].name,
            data: (this.matches as MatchType[])[2].points,
            backgroundColor: colors[2].backgroundColor,
            borderColor: colors[2].borderColor
          },
          {
            label: (this.matches as MatchType[])[3].name,
            data: (this.matches as MatchType[])[3].points,
            backgroundColor: colors[3].backgroundColor,
            borderColor: colors[3].borderColor
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
      this.wines = newVal;

      let ctx = document.getElementById('radar') as ChartItem

      new Chart(ctx, {
        type: 'radar',
        data: {
           labels: ['Süße', 'Säure', 'Alkohol', 'Körper', 'Fruchtigkeit'],
            datasets: [
          {
            label: newVal[0].name,
            data: newVal[0].points,
            backgroundColor: colors[0].backgroundColor,
            borderColor: colors[0].borderColor
          },
          {
            label: newVal[1].name,
            data: newVal[1].points,
            backgroundColor: colors[1].backgroundColor,
            borderColor: colors[1].borderColor
          },
          {
            label: newVal[2].name,
            data: newVal[2].points,
            backgroundColor: colors[2].backgroundColor,
            borderColor: colors[2].borderColor
          },
          {
            label: newVal[3].name,
            data: newVal[3].points,
            backgroundColor: colors[3].backgroundColor,
            borderColor: colors[3].borderColor
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
.ResultChoice {
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
    background-color: #ff8282;
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
  flex-grow: 1;
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
