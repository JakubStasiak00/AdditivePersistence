<template>
    <header>
        <h1>Additive Persistence</h1>
        <p>Calculate the persistence and digital root just like that !</p>
    </header>

    <form action="" @submit.prevent="calculateResult(userInput)">
        <input type="text" v-model="userInput" @input="inputing">
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
const digitalRoot = ref(0)
const numberRegex = /^\d+$/

const inputing = e => {
    if (!numberRegex.test(e.data)) {
        e.target.value = e.target.value.replace(/[^0-9]/g, '')
        userInput.value = e.target.value
    }
}

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
    digitalRoot.value = 0

    let digits = splitIntoArray(n)
    let result = 0

    console.log(digits)

    do {
        if (!(digits.length > 1)) {
            digitalRoot.value = digits[0]
            additionalPersistence.value = 0
            return
        }
        result = calculatingSum(digits)
        digits = splitIntoArray(result)
        additionalPersistence.value++
        console.log(result)
    } while (result >= 10)

    digitalRoot.value = result
}


</script>

<style lang="scss">
#app {
    background-color: rgb(92, 189, 92);
    height: 100vh;
    padding-top: 40%;
    display: flex;
    flex-direction: column;
    gap: 2rem;
    padding-inline: 1rem;
}

body {
    font-family: Helvetica;
    text-align: center;
    margin: 0;
}

form {
    display: flex;
    margin: 0 auto;
    margin-bottom: 2rem;
    width: 100%;
    justify-content: center;
}

@media screen and (min-width: 500px) {

    #app {
        height: auto;
        max-width: 400px;
        position: absolute;
        top: 40%;
        left: 50%;
        transform: translate(-50%, -50%);
        padding: 2rem;

    }
}
</style>