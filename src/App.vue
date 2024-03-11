<script setup>
import { ref } from 'vue'
// import newButton from './components/newButton.vue'

let data = {
    "items":[{"name":"Blade of alacrity", "pic":"/src/img/blade_of_alacrity.jpg"},
        {"name":"Band of elvenskin", "pic":"/src/img/band_of_elvenskin.jpg"},
        {"name":"recipe", "pic":"/src/img/Default_recipe_icon.png"},
        {"name":"Yasha", "pic":"/src/img/yasha.jpg"},
        {"name":"Ogre axe", "pic": "/src/img/ogre_axe.jpg"},
        {"name":"Staff of wizardy", "pic":"/src/img/staff_of_wizardry.jpg"},
        {"name":"Point bооster", "pic":"/src/img/point_booster.jpg"},
        {"name":"Aghanim's scepter", "pic":"/src/img/aghanims_scepter.jpg"},
        {"name":"Shadow blade", "pic":"/src/img/shadow_blade.jpg"},
        {"name":"Broadsword", "pic":"/src/img/broadsword.jpg"},
        {"name":"Shadow amulet", "pic":"/src/img/shadow_amulet.jpg"},
        {"name":"Blitz knuckles", "pic":"/src/img/blitz_knuckles.jpg"},
        {"name":"Crystalys", "pic":"/src/img/crystalys.jpg"},
        {"name":"Blades of attack", "pic":"/src/img/blades_of_attack.jpg"},
        {"name":"Silver edge", "pic":"/src/img/silver_edge.jpg"},
        {"name":"Sages mask", "pic":"/src/img/sages_mask.jpg"},
        {"name":"Circlet", "pic":"/src/img/circlet.jpg"},
        {"name":"Ring of protection", "pic":"/src/img/ring_of_protection.jpg"},
        {"name":"Urn of shadows", "pic":"/src/img/urn_of_shadows.jpg"},
        {"name":"Fluffy hat", "pic":"/src/img/fluffy_hat.jpg"},
        {"name":"Force staff", "pic":"/src/img/force_staff.jpg"},
        {"name":"Belt of strength", "pic":"/src/img/belt_of_strength.jpg"},
        {"name":"Sange", "pic":"/src/img/sange.jpg"},
        {"name":"Cloak", "pic":"/src/img/cloak.jpg"},
        {"name":"Ring of health", "pic":"/src/img/ring_of_health.jpg"},
        {"name":"Ring of regen ", "pic":"/src/img/ring_of_regen.jpg"},
        {"name":"Hood of defian", "pic":"/src/img/hood_of_defiance.jpg"},
        {"name":"Voodoo mask", "pic":"/src/img/voodoo_mask.jpg"},
        {"name":"Eternal shroud", "pic":"/src/img/eternal_shroud.jpg"},
        {"name":"Demon edge", "pic":"/src/img/demon_edge.jpg"}],
    "build": { 
        "3" : [0, 1, 2],
        "7" : [0, 4, 5, 6],
        "8" : [9, 10, 11],
        "12" : [2, 10, 13],
        "14" : [2, 8, 29],
        "18" : [2, 15, 16, 17],
        "20" : [2, 5, 19],
        "22" : [2, 4, 21],
        "26" : [23, 24, 25],
        "28" : [2, 26, 27]
    }
}

let arr = []
let selection = []
const arr2 = ref(arr)
let playerAnswer = ref([])
let finalAnswer=[]
let answerText=ref("")
let displaying = ref("none")

let keyForBuild = Object.keys(data["build"])
let keyRandomBuild = keyForBuild[Math.floor(Math.random() * keyForBuild.length)]
let buildObject = ref(data["items"][keyRandomBuild])
selection.push(data["items"][keyRandomBuild])

for(let i =0; i<6; i++){
  let a=[]
  for(let j=0; j<4; j++){
    let random = Math.floor(Math.random() * data["items"].length)
    while (selection.includes(data["items"][random])){
      random = Math.floor(Math.random() * data["items"].length)
    }
    a.push(data["items"][random])
    selection.push(data["items"][random])
  }
  arr.push(a) 
}

function compareNumbers(a, b){
  return a-b
}

function check(){
  let playerAnswerList = playerAnswer.value
  for(let i=0; i<playerAnswerList.length; i++){
    for(let j=0; j<data["items"].length; j++){
      if(playerAnswerList[i]==data['items'][j]["name"]){
        finalAnswer.push(j)
      }
    }
  }

  if(JSON.stringify(data["build"][keyRandomBuild])===JSON.stringify(finalAnswer.sort(compareNumbers))){
    console.log("УРАААААА")
    answerText.value = "Правильно!"
  }else{
    console.log(":(")
    answerText.value = "Неправильно("
  }
  displaying.value="flex"
  finalAnswer=[]
}
</script>

<template>
  <div class="">
    <img :src="buildObject.pic" alt="" class="build_img">
    <h1>{{ buildObject.name }}</h1>
    <h2 >{{ answerText }}</h2>
  </div>
  <div class="playerChoice">
    <button class="end">Закончить</button>
    <button class="next">Продолжить</button>
  </div>
  <div class="png">
    <div v-for="element in arr2" class="row">
      <div v-for="item in element" class="flex_element">
        <label :for="item.name">  
          <v-card class="mx-auto my-8" max-width="700" :title="item.name" color="#6b6b6b" link>
            <input type="checkbox" :name="item.name" :id="item.name" :value="item.name" v-model="playerAnswer">
            <img :src="item.pic" alt="">
          </v-card>
        </label>
      </div>
    </div>
  </div>
  <button v-on:click="check()">Проверить</button>
  
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.png{
  display: flex;
  flex-direction: row;
}

.row{
  width: 100%;
  display: inline;
}

.flex_element{  
  margin-right: 10px;
}

.build_img{
  width: 150px;
  height: 100px;
}

.playerChoice{
  position: absolute;
  display: v-bind(displaying);
  top: 200px;
  left: 19%;
}

.end{
  margin-right: 300px;
}

.start{
  margin-left: 300px;
}
</style>
