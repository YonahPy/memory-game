<template>
  <main>
    <section>
    
      <Card v-for="item in shuffledCards" :key="item.id" :character-name="item.characterName"  :url-image="item.urlImage" @click="infoCard(item.id, item.characterName)" :matched="matched" @update-matched="handleEmit">
      </Card>
     
  </section>

    
  </main>
</template>


<script setup lang="ts">
import Card from '@/components/Card.vue';
import { ref, onMounted } from 'vue';

interface CardData{
  id: number;
  characterName: string;
  urlImage: string;
}

const cards: CardData[] = [
  { id: 1, characterName: 'Lorian & Lothric', urlImage: 'src/assets/images/twin-princes.jpg' },
  { id: 2, characterName: 'Lorian & Lothric', urlImage: 'src/assets/images/twin-princes.jpg' },
  { id: 3, characterName: 'Vordt', urlImage: 'src/assets/images/vordt.jpg' },
  { id: 4, characterName: 'Vordt', urlImage: 'src/assets/images/vordt.jpg' },
  { id: 5, characterName: 'Wolnir', urlImage: 'src/assets/images/wolnir.jpg' },
  { id: 6, characterName: 'Wolnir', urlImage: 'src/assets/images/wolnir.jpg' },
  { id: 7, characterName: 'Gael', urlImage: 'src/assets/images/gael2.jpg' },
  { id: 8, characterName: 'Gael', urlImage: 'src/assets/images/gael2.jpg' },
  { id: 9, characterName: 'Abyss Watchers', urlImage: 'src/assets/images/abyss-watchers.jpg' },
  { id: 10, characterName: 'Abyss Watchers', urlImage: 'src/assets/images/abyss-watchers.jpg' },
  { id: 11, characterName: 'Aldrich', urlImage: 'src/assets/images/aldrich.jpg' },
  { id: 12, characterName: 'Aldrich', urlImage: 'src/assets/images/aldrich.jpg' },
  { id: 13, characterName: 'Cursed rotted greatwood', urlImage: 'src/assets/images/cursed-rotted.jpg' },
  { id: 14, characterName: 'Cursed rotted greatwood', urlImage: 'src/assets/images/cursed-rotted.jpg' },
  { id: 15, characterName: 'Dancer of the boreal valley', urlImage: 'src/assets/images/dancer.jpg' },
  { id: 16, characterName: 'Dancer of the boreal valley', urlImage: 'src/assets/images/dancer.jpg' },
  { id: 17, characterName: 'Deacons of the deep', urlImage: 'src/assets/images/deacons.jpg' },
  { id: 18, characterName: 'Deacons of the deep', urlImage: 'src/assets/images/deacons.jpg' },
  { id: 19, characterName: 'Demon Prince', urlImage: 'src/assets/images/demon-prince.jpg' },
  { id: 20, characterName: 'Demon Prince', urlImage: 'src/assets/images/demon-prince.jpg' },
  { id: 21, characterName: 'Dragonslayer Armor', urlImage: 'src/assets/images/dragonslayer.jpg' },
  { id: 22, characterName: 'Dragonslayer Armor', urlImage: 'src/assets/images/dragonslayer.jpg' },
  { id: 23, characterName: 'Sister Friede', urlImage: 'src/assets/images/friede.jpg' },
  { id: 24, characterName: 'Sister Friede', urlImage: 'src/assets/images/friede.jpg' },
  { id: 25, characterName: 'Champions Gravetender', urlImage: 'src/assets/images/gravetender.jpg' },
  { id: 26, characterName: 'Champions Gravetender', urlImage: 'src/assets/images/gravetender.jpg' },
  { id: 27, characterName: 'Gundyr', urlImage: 'src/assets/images/gundyr.jpg' },
  { id: 28, characterName: 'Gundyr', urlImage: 'src/assets/images/gundyr.jpg' },
  { id: 29, characterName: 'Midir', urlImage: 'src/assets/images/midir.jpg' },
  { id: 30, characterName: 'Midir', urlImage: 'src/assets/images/midir.jpg' },
  { id: 31, characterName: 'Nameless king', urlImage: 'src/assets/images/nameless-king.jpg' },
  { id: 32, characterName: 'Nameless king', urlImage: 'src/assets/images/nameless-king.jpg' },
  { id: 33, characterName: 'Oceiros', urlImage: 'src/assets/images/oceiros.jpg' },
  { id: 34, characterName: 'Oceiros', urlImage: 'src/assets/images/oceiros.jpg' },
  { id: 35, characterName: 'Old demon', urlImage: 'src/assets/images/old-demon.png' },
  { id: 36, characterName: 'Old demon', urlImage: 'src/assets/images/old-demon.png' },
  { id: 37, characterName: 'Crystal Sage', urlImage: 'src/assets/images/sage.jpeg' },
  { id: 38, characterName: 'Crystal Sage', urlImage: 'src/assets/images/sage.jpeg' },
  { id: 39, characterName: 'Soul of cinder', urlImage: 'src/assets/images/soul-of-cinder.jpg' },
  { id: 40, characterName: 'Soul of cinder', urlImage: 'src/assets/images/soul-of-cinder.jpg' },
  { id: 41, characterName: 'Pontiff Sulyvahn', urlImage: 'src/assets/images/sulyvahn.png' },
  { id: 42, characterName: 'Pontiff Sulyvahn', urlImage: 'src/assets/images/sulyvahn.png' },
  { id: 43, characterName: 'Yhorm', urlImage: 'src/assets/images/yhorm.jpg'},
  { id: 44, characterName: 'Yhorm', urlImage: 'src/assets/images/yhorm.jpg'}
  
]

const shuffledCards = ref<CardData[]>([]);

let firstCard = ref<{id:number; name: string}[]>([])
let matched = ref<string>('nothing')

onMounted(() => {
  shuffledCards.value = shuffledArray(cards)
})

function shuffledArray(array: CardData[]): CardData[]{
  const shuffled = [...array];
  for (let i = shuffled.length - 1; i > 0; i--){
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]]
  }
  return shuffled
}


function infoCard(id:number, name: string): void{
  firstCard.value.push({id, name})
  if(firstCard.value.length === 2){
    if(firstCard.value[0].name === firstCard.value[1].name && firstCard.value[0].id !== firstCard.value[1].id){
      matched.value = 'true'
    }
    console.log(matched.value)
    firstCard.value.splice(0, firstCard.value.length)
    matched.value = 'false'
    
  } 
}

function handleEmit(nothing: string): void{
  matched.value = nothing
  console.log(matched.value)
}
</script>

<style>
body{
  background-color: darkslategray;
}
main{
  margin-top: 5vh;
  margin-inline: 5vw;
}
section{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  gap: 20px;
}
</style>