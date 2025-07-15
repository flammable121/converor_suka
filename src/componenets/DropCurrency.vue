<template>
    <div class="select-drop">
        <ul class="select-drop__ul">
            <li
            class="select-drop__li"
            v-for="currency in currencies" 
            :key="currency"
            @click="selectCurrency(currency)"
            >
            {{ currency }}
            </li>
        </ul>
    </div>
</template>

<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

const emit = defineEmits(['currency-selected'])

const rates = ref({})
const currencies = ref ([])
const selectedCurrency = ref('')

const selectCurrency = (currency) => {
    selectedCurrency.value = currency
    emit('currency-selected', currency)
}


onMounted(async() => {
    const response = await axios.get('https://api.currencyfreaks.com/v2.0/rates/latest?apikey=a9e13e0f86234e5caa2e8a0dad0d2a66')

    rates.value = response.data.rates
    currencies.value = Object.keys(rates.value)
});




</script>

<style>
.select-drop {
    font-family: "Gothic";
    font-size: 24px;
    background-color: white;
    position: absolute;
    z-index: 1000;
    height: 500px;
    width: 1658px;
    overflow: auto;
    padding: 0px 20px;
    border: solid 1px #E6E6E6;
}

.select-drop::-webkit-scrollbar {
    display: none;
}
.select-drop__ul {
    columns: 6;
}
.select-drop__li {
    list-style: none;
}
</style>
