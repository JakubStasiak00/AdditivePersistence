<template>
    <input type="number">
    <table>
        <tr>
            <th>Iteration</th>
            <th>Sum</th>
        </tr>
        <tr>
            <td>dummy</td>
            <td>dummy</td>
        </tr>
    </table>
</template>

<script setup>
import { ref } from 'vue';

    const userInput = ref(null)
</script>

<style lang="scss">
    body {
        font-family: Helvetica;
    }

    input {
        display: block;
        margin: 0 auto;
        margin-top: 20vh;
        margin-bottom: 2rem;
    }

    table {
        border-collapse: collapse;
        font-size: 1.5rem;
        margin: 0 auto;
    }

    tr + tr {
        border-top: 2px solid black;
    }

</style>