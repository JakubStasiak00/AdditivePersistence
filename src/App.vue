<template>
    <form action="" @submit.prevent="calculateResult(userInput)">
        <input type="number" v-model="userInput">
        <button>Calculate</button>
    </form>

    <div class="result">
        <div class="persistence">
            The additional persistence is: <span> {{ additionalPersistence }} </span>
        </div>
        <div class="addRoot">
            The digital root is: <span> {{ digitalRoot }} </span>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const userInput = ref(null)
const additionalPersistence = ref(0)
const digitalRoot = ref(null)

function splitIntoArray(num) {
    return Array.from(String(num), Number);
}

const calculatingSum = arr => {
    let sum = 0

    for (let i = 0; i < arr.length; i++) {
        sum += arr[i]
    }

    return sum
}

const calculateResult = n => {
    additionalPersistence.value = 0
    digitalRoot.value = null

    let digits = splitIntoArray(n)
    let result = 0

    do {
        result = calculatingSum(digits)
        digits = splitIntoArray(result)
        additionalPersistence.value++
        console.log(result)
    } while (result >= 10)

    digitalRoot.value = result
}


</script>

<style lang="scss">
body {
    font-family: Helvetica;
}

form {
    display: flex;
    margin: 0 auto;
    margin-top: 20vh;
    margin-bottom: 2rem;
    width: 100%;
    justify-content: center;
}
</style>