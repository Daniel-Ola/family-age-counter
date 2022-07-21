<script setup>
import { ref, computed, watch } from "vue"
import { WITH_CTX } from "@vue/compiler-dom";

const currentAge = ref(0)
const wives = ref(0)
const children = ref(0)
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
const ch = computed(() => {
  let ages = [];
  for(let i = 0; i < children.value; i++ ) {
    const age = currentAge.value - generateRandomAge(20, currentAge.value)
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
const toggler = ref(true)

</script>

<template>


<div style="display: flex;" :class="[toggler ? 'align-bottom' : 'align-top' ]">
  <button
    :disabled="currentAge < 1"
    @click="toggler = !toggler"
    class="toggle-btn"
  >
    Toggle View
  </button>
	
	<div style="padding: 10px;" v-if="toggler" class="form-container">
    <div>
      <label for="currentAge">current user age</label>
		  <input type="number" inputmode="numeric" id="currentAge" v-model="currentAge">
    </div>
    <div style="display: flex; gap: 1rem">
      <div>
        <label for="wives">No of Wife(ves)</label>
        <input id="wives" type="number" v-model="wives">
      </div>
      <div>
        <label for="children">No. of Children</label>
        <input id="children" type="number" v-model="children">
      </div>
    </div>
		
    <div style="display: flex; gap: 1rem">
      <div>
        <label for="eldersibs">No. of Elder Siblings</label>
        <input type="number" inputmode="numeric" id="eldersibs" v-model="elderSibs">
      </div>
      <div>
        <label for="elderSibs">No. of Younger Siblings</label>
        <input type="number" inputmode="numeric" id="elderSibs" v-model="youngerSibs">
      </div>
    </div>
    <div class="form-group">
      <div class="has-checkbox">
        <label for="hasFather" style="text-align: center">hasFather</label>
        <input type="checkbox" id="hasFather" v-model="hasFather">
      </div>
      <div class="has-checkbox">
        <label for="hasMother" style="text-align: center">hasMother</label>
        <input type="checkbox" id="hasMother" v-model="hasMother">
      </div>
    </div>
    <div class="form-group">
      <div class="has-checkbox">
        <label for="hasPGMother" style="text-align: center">hasPGMother</label>
        <input type="checkbox" id="hasPGMother" v-model="hasPGMother" />
      </div>
      <div class="has-checkbox">
        <label for="hasPGFather" style="text-align: center">hasPGFather</label>
        <input type="checkbox" id="hasPGFather" v-model="hasPGFather" />
      </div>
    </div>
    <div class="form-group">
      <div class="has-checkbox">
        <label for="hasMGMother" style="text-align: center">hasMGMother</label>
        <input type="checkbox" id="hasMGMother" v-model="hasMGMother" />
      </div>
      <div class="has-checkbox">
        <label for="hasMGFather" style="text-align: center">hasMGFather</label>
        <input type="checkbox" id="hasMGFather" v-model="hasMGFather" />
      </div>
    </div>
    <!-- <p>
      <input type="checkbox" id="checkbox" v-model="checked" />
      <label for="checkbox">{{ checked }}</label>
    </p>-->
	</div>

	<div v-else>
		<p>Current Age {{ getYearOfBirth(currentAge) }} </p>
		<p>Wives Age {{ wa }} </p>
		<p>Children Age {{ ch }} </p>
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

label {
  display: block;
  margin-bottom: 0.25rem;
}

.form-group {
  display: flex;
  gap: 1rem;
  /* justify-content: space-between; */
  align-items: center;
}

.form-group > .has-checkbox {
  display: flex;
  flex-basis: 50%;
  align-items: center;
}

/* .form-group > .has-checkbox:first-child {
  border: 2px solid red;
} */

/* .form-group > .has-checkbox > label {
  border: 2px solid red;
  flex-grow: 1;
} */

.has-checkbox > label {
  display: inline;
}

input {
  height: 2rem;
  text-align: center;
  width: 100%;
}

.form-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.align-bottom {
  flex-direction: column;
  /* -reverse; */
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

.align-top {
  flex-direction: column;
  justify-content: space-between;
  gap: 1rem;
  align-items: center;
}

.toggle-btn {
  background-color: blue;
  color: white;
  border-radius: 5px;
  border: transparent;
  padding: 0.5rem;
  width: 7rem;
  cursor: pointer;
}

.toggle-btn:hover {
  background-color: slateblue;
}

.toggle-btn:disabled {
  cursor: not-allowed;
  background-color: grey;
  background-blend-mode: lighten;
}

</style>
