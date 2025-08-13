<template>
    <div class="converter">
        <div class="converter__inner">
            <h3 class="converter__title">Конвертер валют</h3>
            <div class="converter__box">
                <currency-input
                    :title="'У меня есть'"
                    :quick-currencies="quickCurrenciesFrom" 
                    :currencies="currencies"
                    :selectedCurrency="fromCurrency"
                    :amount="amountFrom"
                    :targetCurrency="toCurrency"
                    @updateAmount="val => amountFrom = val"
                    :dropVisible="dropVisible"
                    @currencySelected="onFromCurrencySelected"
                    :rates="rates"
                />
                <div class="box--array">
                    <svg xmlns="http://www.w3.org/2000/svg" width="70" height="88" viewBox="0 0 70 88" fill="none">
                        <path d="M23.6443 48.4825L45.6784 26.4483C46.0689 26.0578 46.069 25.4247 45.6784 25.0341L23.6443 2.99999" stroke="black" stroke-width="4" stroke-linecap="square"/>
                        <path d="M46.5707 39.6822L24.5365 61.7163C24.146 62.1069 24.146 62.74 24.5365 63.1305L46.5707 85.1647" stroke="black" stroke-width="4" stroke-linecap="square"/>
                    </svg>
                </div>
                <currency-input
                    :title="'Хочу приобрести'"
                    :quick-currencies="quickCurrenciesTo"
                    :currencies="currencies"
                    :selectedCurrency="toCurrency"
                    :amount="amountTo"
                    :targetCurrency="fromCurrency"
                    @updateAmount="val => amountTo = val"
                    :dropVisible="dropVisible"
                    @currencySelected="onToCurrencySelected"
                    :rates="rates"
                />
            </div>
        </div>
    </div>
</template>

<script setup>
import CurrencyInput from './components/CurrencyInput.vue';
import { onMounted, ref, watch } from 'vue';
import axios from 'axios';

const rates = ref({})
const currencies = ref([])

const quickCurrenciesFrom = ref([])
const quickCurrenciesTo = ref([])

const fromCurrency = ref('')
const toCurrency = ref('')

const amountFrom = ref('')
const amountTo = ref('')

onMounted(async () => {
    try {
        const response = await axios.get('https://api.currencyfreaks.com/v2.0/rates/latest?apikey=09b7cece3b0840b3b2d908bc4aed72a7')
        rates.value = response.data.rates
        currencies.value = Object.keys(rates.value)

        quickCurrenciesFrom.value = ['USD','EUR','KZT']
        quickCurrenciesTo.value = ['UAH','RUB','KZT']

        fromCurrency.value = 'USD'
        toCurrency.value = 'RUB'


    } catch (error) {
        console.error('Ошибка загрузки данных', error)
    }
});

function onFromCurrencySelected(payload) {
    fromCurrency.value = payload.code

    quickCurrenciesFrom.value = [...quickCurrenciesFrom.value]
    quickCurrenciesFrom.value[payload.index] = payload.code
}

function onToCurrencySelected(payload) {
    toCurrency.value = payload.code

    quickCurrenciesTo.value = [...quickCurrenciesTo.value]
    quickCurrenciesTo.value[payload.index] = payload.code
}

function recalcToAmount() {
    if (!fromCurrency.value || !toCurrency.value || amountFrom.value === '') {
        amountTo.value = '';
        return;
    }

    const rateFrom = rates.value[fromCurrency.value];
    const rateTo = rates.value[toCurrency.value];

    const amountInUSD = amountFrom.value / rateFrom;
    const result = amountInUSD * rateTo;

    amountTo.value = Number(result).toFixed(2);
}

watch([fromCurrency, toCurrency, amountFrom], recalcToAmount, {immediate: true})
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
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;

    .converter__inner {
        display: flex;
        flex-direction: column;
        position: relative;

        .converter__title {
            font-size: 4rem;
            margin: 3.9rem 0;
        }
    
        .converter__box {
            display: flex;
            justify-content: space-between;
            width: 100%;

            .box--array {
                display: flex;
                justify-content: center;
                align-items: flex-end;
                padding-bottom: 7.5rem;
            }
        }
    }
}

@media (max-width:1500px) {
    .converter {
        scale: 0.9;
    }
}
@media (max-width:1400px) {
    .converter {
        scale: 0.7;
    }
}
@media (max-width:1100px) {
    .converter {
        scale: 0.6;
    }
}
@media (max-width:1000px) {
    .converter {
        scale: 0.5;
    }
}
@media (max-width:800px) {
    .converter {
        scale: 0.4;
    }
}
@media (max-width:620px) {
    .converter {
        scale: 0.3;
    }
}
</style>