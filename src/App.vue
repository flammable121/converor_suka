<template>
    <div class="converter">
        <div class="converter__inner">
            <h3 class="converter__title">Конвертер валют</h3>
            <div class="converter__box">
                <currency-input
                    :dropVisible="dropVisible"
                />
                <div class="converter__array">
                    <svg xmlns="http://www.w3.org/2000/svg" width="70" height="88" viewBox="0 0 70 88" fill="none">
                        <path d="M23.6443 48.4825L45.6784 26.4483C46.0689 26.0578 46.069 25.4247 45.6784 25.0341L23.6443 2.99999" stroke="black" stroke-width="4" stroke-linecap="square"/>
                        <path d="M46.5707 39.6822L24.5365 61.7163C24.146 62.1069 24.146 62.74 24.5365 63.1305L46.5707 85.1647" stroke="black" stroke-width="4" stroke-linecap="square"/>
                    </svg>
                </div>
                <currency-input
                    :dropVisible="dropVisible"
                />
            </div>
                <drop-currency
                    v-if="currencyDropVisible"
                    :loadingCurrency="loadingCurrency"
                    :currencies="currencies"
                />
        </div>
    </div>
</template>

<script setup>
import CurrencyInput from './componenets/CurrencyInput.vue';
import DropCurrency from './componenets/DropCurrency.vue';
import { onMounted, ref } from 'vue';
import axios from 'axios';

const rates = ref({})
const currencies = ref([])
const currencyDropVisible = ref(false)
const dropVisible = () => {
    currencyDropVisible.value = !currencyDropVisible.value
}
const loadingCurrency = ref(true)

onMounted(async () => {
    try {
    const response = await axios.get('https://api.currencyfreaks.com/v2.0/rates/latest?apikey=09b7cece3b0840b3b2d908bc4aed72a7')

    rates.value = response.data.rates
    currencies.value = Object.entries(rates.value)   
    } catch (error) {
        console.error('Ошибка загрузки данных', error)
    } finally {
        loadingCurrency.value = false
    }
});
</script>

<style lang="scss">
* {
    font-family: "Gothic";
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.converter {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;

    .converter__inner {
        display: flex;
        flex-direction: column;
        width: 100%;
        max-width: 110rem;
        position: relative;

        .converter__title {
            font-size: 4rem;
            margin: 3.9rem 0;
        }
    
        .converter__box {
            display: flex;
            justify-content: space-between;

            .converter__array {
                display: flex;
                justify-content: center;
                align-items: end;
                padding-bottom: 7.5rem;
            }
        }
    }
}
</style>