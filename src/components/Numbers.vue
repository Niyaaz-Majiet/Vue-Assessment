<script setup lang="ts">
import { ref } from 'vue';

let limit : number = ref(100);

function getRandomNumberOrderList(limit:number)
{
	limit = limit;
	let numbers : number[] = [];
	for(var i = 0; i < limit; i++) { numbers = [...numbers, (i+1)]; }

	return numbers.sort(() => Math.random() - 0.5);
}

function onNumberHover(number:number) {
  const numbers : any = document.querySelectorAll('.number');

  for(let i = 0; i < numbers.length; i++)
  {
    const num = numbers[i].textContent.trim();
    if(number % num === 0)
    {
		numbers[i].classList.add('active');
    }
  }
}

function reset()
{
	const numberElements = document.querySelectorAll('.number');
	numberElements.forEach(num => num.classList.remove('active'))
}
</script>

<template>
	<div>
		<input type="number" v-model="limit"/><br /><br />
		<div class="number"
			:id="'number-'+number"
			v-for="number in getRandomNumberOrderList(limit)"
			:key="number"
			@mouseover="() => onNumberHover(number)"
			@mouseout="() => reset()"
		>
			{{ number }}
		</div>
	</div>
</template>