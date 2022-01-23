/*
{
name: 'Carménère',
color: 'Rosé',
taste: '90%',
aroma: '10%',
speak: 'Kar-me-nähr',
points: [1,3,3,3,4]
},
*/

<template>
  <div class="WineComponent">
    <div class="row">
      <span class="name">{{ wine.name }}</span><span class="speak">[ {{ wine.speak }} ]</span>
      <div class="color">{{ wine.color }}</div>
    </div>
    <div class="row horizontal">
      <img v-if="assetPath" :src="assetPath + '/wineicon.png'" />
      <div class="ratings">
        It's a match ...
        <div class="progressBg">
          <span class="progressBar" :style="{width: wine.taste + '%'}"></span>
        </div>
        <div class="percText"><span class="perc">{{wine.taste}}%</span> ... für dich</div>
        <div class="progressBg">
          <span class="progressBar" :style="{width: wine.aroma + '%'}"></span>
        </div>
        <div class="percText"><span class="perc">{{wine.aroma}}%</span> ... zum Essen</div>
      </div>
      <div class="button">Wein kaufen</div>
    </div>


  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from "vue";

export default defineComponent({
  name: 'WineComponent',
  inject: ['assetPath'],
  props: {
    wine: {
      type: Object as any
    }
  }
});
</script>

<style scoped lang="scss">
.WineComponent {
  flex-direction: column;
  flex-flow: column wrap;
  justify-content: space-around;
  display: flex;
  margin-bottom: 10px;
  background-color: white;
  padding: 10px;
  border: 1px solid lightgrey;
  border-radius: 5px;
  position: relative;
}

.horizontal{
  display: flex;
  flex-flow: row nowrap;
}

.button {
  cursor: pointer;
  background-color: #f67e7d;
  margin: 70px auto 0 110px;
  border: none;
  color: #fff;
  border-radius: 30px;
  max-width: 225px;
  padding: 5px 25px 5px;
  text-transform: uppercase;
  font-size: 12px;
  height: 20px;

  &:hover {
    background-color: #ff8282;
  }
}

.name{
  color: grey;
  font-weight: 500;
  font-size: 16px;
}

.speak {
  margin-left: 20px;
  color: gray;
}

.color {
  background-color: #ff8282;
  padding: 5px 10px;
  display: inline-block;
  position: absolute;
  right: 10px;
  color: white;
  top: 10px;
}
img {
  height: 100px;
  border: 1px solid lightgray;
  border-radius: 5px;
}

.row{
  margin-bottom: 5px;
}

.ratings {
  margin-left: 30px;
  font-weight: bold;
  color: grey;
}

.perc {
  color: #631841;
  font-weight: normal;
}

.percText {
  font-weight: normal;
  margin-bottom: 10px;
}

.progressBg{
  background-color: grey;
  border-radius: 10px;
  height: 6px;
  width: 100%;
  margin: 5px 0;
  position: relative;
}

.progressBar {
  background-color: #631841;
  display: inline-block;
  position: absolute;
  top: 0;
  height: 5px;
  border-radius: 10px;
}
</style>
