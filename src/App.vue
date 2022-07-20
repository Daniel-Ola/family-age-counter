<script setup>
import { ref, computed, watch } from "vue"
import { WITH_CTX } from "@vue/compiler-dom";

const currentAge = ref(0)
const wives = ref(0)
const elderSibs = ref(0)
const youngerSibs = ref(0)
const hasFather = ref(false)
const hasMother = ref(false)
const hasPGMother = ref(false)
const hasPGFather = ref(false)
const hasMGMother = ref(false)
const hasMGFather = ref(false)



const wa = computed(() => {
  let ages = [];
  for(let i = 0; i < wives.value; i++ ) {
    const age = currentAge.value - (Math.floor(Math.random() * 7))
    ages.push(getYearOfBirth(age))
  }
  return ages.sort(function(a, b){return a - b});
})

const es = computed(() => {
  let ages = [];
  for(let i = 0; i < elderSibs.value; i++ ) {
    const min = generateRandomAge(2, 3);
    const max = min * elderSibs.value
    const age = currentAge.value + (Math.floor(Math.random() * elderSibs.value * 2))+2
    // const age = currentAge.value + generateRandomAge(min, max)
    ages.push(getYearOfBirth(age))
  }
  return ages.sort(function(a, b){return a - b});
})

const ys = computed(() => {
  let ages = [];
  for(let i = 0; i < youngerSibs.value; i++ ) {
    const min = generateRandomAge(2, 3);
    const max = min * youngerSibs.value
    const age = currentAge.value - (Math.floor(Math.random() * youngerSibs.value * 2))-2
    // const age = currentAge.value - generateRandomAge(min, max)
    ages.push(getYearOfBirth(age))
    // ages.push(age)
  }
  return ages.sort(function(a, b){return a - b});
})

const fa = ref(0)
const ma = ref(0)
const pgm = ref(0)
const pgp = ref(0)
const mgm = ref(0)
const mgp = ref(0)
watch(hasFather, () => {
  if(hasFather.value) {
    fa.value = currentAge.value + generateRandomAge(20, 25)
  } else {
    fa.value = 0;
  }
})

watch(hasMother, () => {
  if(hasMother.value) {
    if(hasFather.value) {
      ma.value = fa.value - generateRandomAge(3, 7)
    } else {
      ma.value = currentAge.value + generateRandomAge(20, 25)
    }
  } else {
    ma.value = 0;
  }
})

watch(hasPGMother, () => {
  if(hasPGMother.value) {
    pgm.value = currentAge.value + generateRandomAge(40, 45)
  } else {
    pgm.value = 0;
  }
})

watch(hasPGFather, () => {
  if(hasPGFather.value) {
    pgp.value = currentAge.value + generateRandomAge(45, 50)
  } else {
    pgp.value = 0;
  }
})

watch(hasMGMother, () => {
  if(hasMGMother.value) {
    mgm.value = currentAge.value + generateRandomAge(40, 45)
  } else {
    mgm.value = 0;
  }
})

watch(hasMGFather, () => {
  if(hasMGFather.value) {
    mgp.value = currentAge.value + generateRandomAge(45, 50)
  } else {
    mgp.value = 0;
  }
})

const generateRandomAge = (min, max) => {
  // find diff
    let difference = max - min;

    // generate random number 
    let rand = Math.random();

    // multiply with difference 
    rand = Math.floor( rand * difference);

    // add with min value 
    rand = rand + min;

    return rand;
}

const getYearOfBirth = (age) => {
  const d = new Date();
  const thisYear = d.getFullYear();
  return thisYear - age;
}

console.log(getYearOfBirth(23))

const checked = ref(false)

</script>

<template>


<div style="display: flex;">
	
	<div style="flex-basis: 50%;">
		current user age
		<input type="number" v-model="currentAge">

		<p><input type="number" v-model="wives"> wife(ves)</p>
		<p><input type="number" v-model="elderSibs">	elder sibs</p>
		<p><input type="number" v-model="youngerSibs">	younger sibs</p>

		<p>
      <input type="checkbox" id="hasFather" v-model="hasFather">
      <label for="hasFather">has Father</label>
    </p>

		<p>
      <input type="checkbox" id="hasMother" v-model="hasMother">
      <label for="hasMother">has Mother</label>
    </p>
    <p>
      <input type="checkbox" id="hasPGMother" v-model="hasPGMother" />
      <label for="hasPGMother">hasPGMother</label>
    </p>
    <p>
      <input type="checkbox" id="hasPGFather" v-model="hasPGFather" />
      <label for="hasPGFather">hasPGFather</label>
    </p>
    <p>
      <input type="checkbox" id="hasMGMother" v-model="hasMGMother" />
      <label for="hasMGMother">hasMGMother</label>
    </p>
    <p>
      <input type="checkbox" id="hasMGFather" v-model="hasMGFather" />
      <label for="hasMGFather">hasMGFather</label>
    </p>
    <!-- <p>
      <input type="checkbox" id="checkbox" v-model="checked" />
      <label for="checkbox">{{ checked }}</label>
    </p>-->
	</div>

	<div>
		<p>Current Age {{ getYearOfBirth(currentAge) }} </p>
		<p>Wives Age {{ wa }} </p>
		<p>Elder sibs {{ es }} </p>
		<p>Younger sibs {{ ys }} </p>
		<p>Father {{ getYearOfBirth(fa) }} </p>
		<p>Mother {{ getYearOfBirth(ma) }} </p>
		<p>PGM {{ getYearOfBirth(pgm) }} </p>
		<p>PGP {{ getYearOfBirth(pgp) }} </p>
		<p>MGM {{ getYearOfBirth(mgm) }} </p>
		<p>MGP {{ getYearOfBirth(mgp) }} </p>
	</div>

</div>



</template>

<style scoped>




</style>
