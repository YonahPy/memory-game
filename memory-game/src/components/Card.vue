<template>
<div class="card">
		<div class="card__inner" :class="{'is-flipped': isFlipped}" @click="turnCard">
			<div class="card__face card__face--front">
				
			</div>
			<div class="card__face card__face--back">
				<div class="card__content" :style="{backgroundImage: `url(${urlImage})`}">
					<p>{{ characterName }}</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const prop = defineProps({
    urlImage: {type: String, required: true},
    characterName: {type: String, required: true},
    matched: {type: Boolean}
})
let isFlipped = ref<boolean>(false)

const emit = defineEmits<{
  clickedCard: [isFlipped: boolean]
}>()

function turnCard(){
    isFlipped.value = !isFlipped.value
    emit('clickedCard', isFlipped.value)
    if(!prop.matched){
      isFlipped.value = false
    }
}
</script>

<style>
:root {
  --primary: #FFCE00;
  --secondary: #FE4880;
  --dark: #212121;
  --light: #F3F3F3;
}

* {
  margin: 0;
  padding: 0;
}


.card {
  width: 100px;
  height: 150px;
  perspective: 1000px;
  
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card__inner.is-flipped {
  transform: rotateY(180deg);
}


.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 16px;
  box-shadow: 0px 3px 18px 3px rgba(0, 0, 0, 0.2);
}

.card__face--front {
  background-size: cover;
  background-image: url('../assets/images/dark-souls-3-cinder.jpg');
 
}

.card__face--front h2 {
  color: #FFF;
  font-size: 20px;
  padding-inline: 10px;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(180deg);
}

.card__content {
  width: 100%;
  height: 100%;
  background-size: cover;
  display: flex;
  align-items: end;
  margin-bottom: 10px;
  
}
.card__content p{
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
    color: white;
    font-size: 12px;
    font-weight: bold;
    padding-left: 15px;
    padding-bottom: 5px;
    
}

</style>