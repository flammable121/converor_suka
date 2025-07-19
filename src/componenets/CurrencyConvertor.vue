<template>
  <div class="currency-converter">
      <h3 class="currency-converter__title">Конвертер валют</h3>
      <div class="currency-converter__convertor">
        <div class="convertor__input">
          <p class="convertor__input--name">У меня есть</p>
          <div class="convertor__input--currency">
          <button class="currency--btn">{{ selectedCurrencyFrom }}</button>
          <button class="currency--btn">{{ selectedCurrencyFrom }}</button>
          <button class="currency--btn">{{ selectedCurrencyFrom }}</button>
          <span
          @click="selectCurrency('from')"
          class="currency--btn">
            <svg xmlns="http://www.w3.org/2000/svg" width="52" height="28"      viewBox="0 0 52 28" fill="none">
              <path d="M3.18811 3.00348L25.2222 25.0376C25.6128 25.4281 26.2459 25.4281 26.6365 25.0376L48.6706 3.00348" stroke="#C05406" stroke-width="4" stroke-linecap="square"/>
            </svg>
          </span>
        </div>
          <DropCurrency
            v-if="showCurrencyList"
            class="drop__currency"
            @currency-selected="handleCurrencySelected"
          />
        <div class="convertor__block--input">
          <p class="input__p">Казахстанский тенге</p>
          <input class="input__input" type="text" v-model="amountFrom">
          <p
           
          class="input__currency">{{ selectedCurrencyFrom }} = </p>
        </div>
      </div>
      <div class="array">
        <svg xmlns="http://www.w3.org/2000/svg" width="70" height="88" viewBox="0 0 70 88" fill="none">
          <path d="M23.6443 48.4825L45.6784 26.4483C46.0689 26.0578 46.069 25.4247 45.6784 25.0341L23.6443 2.99999" stroke="black" stroke-width="4" stroke-linecap="square"/>
          <path d="M46.5708 39.6822L24.5367 61.7163C24.1461 62.1069 24.1461 62.74 24.5367 63.1305L46.5708 85.1647" stroke="black" stroke-width="4" stroke-linecap="square"/>
        </svg>
      </div>
<!--    <div class="convertor__input">
        <p class="convertor__input--name">Хочу приобрести</p>
          <div class="convertor__input--currency">
            <button class="currency--btn">{{ selectedCurrencyTo }}</button>
            <button class="currency--btn">{{ selectedCurrencyTo }}</button>
            <button class="currency--btn">{{ selectedCurrencyTo }}</button>
            <span 
            @click="selectCurrency('to')"
            class="currency--btn">
              <svg xmlns="http://www.w3.org/2000/svg" width="52" height="28" viewBox="0 0 52 28" fill="none">
                <path d="M3.18811 3.00348L25.2222 25.0376C25.6128 25.4281 26.2459 25.4281 26.6365 25.0376L48.6706 3.00348" stroke="#C05406" stroke-width="4" stroke-linecap="square"/>
              </svg>
          </span>
        </div>
        <div class="convertor__block--input">
          <p class="input__p">Казахстанский тенге</p>
          <input class="input__input" type="text" v-model="amountTo">
          <p class="input__currency">1 USD = 468.27 KZT</p>
        </div>
      </div> -->
      <currency-input></currency-input>
    </div>
  </div>
  
  

</template>

<script setup>
import CurrencyInput from './CurrencyInput.vue';
import DropCurrency from './DropCurrency.vue';
import { ref } from 'vue'; 

const showCurrencyList = ref(false)
const selectedCurrencyFrom = ref('USD')
const selectedCurrencyTo = ref('KZT')
const currencyDropdown = ref(null)

const selectCurrency = (type) => {
    currencyDropdown.value = type
    showCurrencyList.value = true
}

const handleCurrencySelected = (currency) => {
   if (currencyDropdown.value === 'from') {
    selectedCurrencyFrom.value = currency
   } else if (currencyDropdown.value === 'to') {
    selectedCurrencyTo.value = currency
   }

   showCurrencyList.value = false
   currencyDropdown.value = null
}


</script>

<style scoped>
.currency-converter {
    width: 100%;
    height: 100%;
}
.currency-converter__convertor {
    display: flex;
    justify-content: center;
}
.currency-converter__title {
    font-size: 64px;
    text-align: center;
}
.convertor__input {
    width: 733px;
    margin: 50px;

}
.array {
    display: flex;
    flex-direction: column;
    justify-content: center;
}
.convertor__input--name {
    font-size: 36px;
    color: #C05406;
}
.convertor__input--currency {
    display: flex;
}
.currency--btn {
    border: 1px solid #CDCDCD;
    font-size: 36px;
    padding: 29px 60px;
    position: relative;
}
.currency--btn:focus {
    background-color: #C05406;
}
.convertor__block--input {
    display: flex;
    flex-direction: column;
}
.input__p {
    font-size: 36px;
}
.input__input {
    font-size: 100px;
    border: none;
}
.input__currency {
    font-size: 24px;
}
.drop__currency {

}
</style>