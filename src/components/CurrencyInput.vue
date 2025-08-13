<template>
<div class="convertor__input">
    <p class="convertor__input--name">{{ props.title }}</p>
        <div class="convertor__input--currency">
            <button 
              v-for="(code, index) in props.quickCurrencies"
              @click="onButtonClicked(code, index)"
              :key="code"
              :class="{ active: activeButton === index }"
              class="currency--btn"
            >
              {{ code }}
            </button>
            <span 
            @click="toggleDropdown"
            class="currency--array">
                <svg xmlns="http://www.w3.org/2000/svg" width="52" height="28" viewBox="0 0 52 28" fill="none">
                    <path d="M3.18811 3.00348L25.2222 25.0376C25.6128 25.4281 26.2459 25.4281 26.6365 25.0376L48.6706 3.00348" stroke="#C05406" stroke-width="4" stroke-linecap="square"/>
                </svg>
            </span>
        </div>
    <div class="convertor__block--input">
      <drop-currency
        v-if="dropVisible"
        :currencies="currencies"
        @currencySelected="selectCurrency"
      />
        <p 
          class="input__p"
          v-if="props.selectedCurrency"
        >
          {{ currencyNames[props.selectedCurrency] || props.selectedCurrency }}
        </p>
        <input
          class="input__input" 
          type="number"
          :value="amount"
          @input="onInput"
        >
        <p class="input__p">{{ rateDisplay }}</p>
    </div>
</div>
</template>

<script setup>
import { computed, ref, watch } from 'vue';
import DropCurrency from './DropCurrency.vue';
import { currencyNames } from '@/cyrrencyNames';

const props = defineProps({
  title: {
    type: String,
    default: 'У меня есть'
  },
  currencies: Array,
  quickCurrencies: Array,
  selectedCurrency: String,
  amount: String,
  targetCurrency: String,
  rates: Object
});

const lastClickedIndex = ref(0)
const activeButton = ref(null)

const dropVisible = ref(false);
const toggleDropdown = () => {
  dropVisible.value = !dropVisible.value
};

const selectCurrency = ( code ) => {
  emit('currencySelected', {
    code,
    index: lastClickedIndex.value
  })
  console.log('Выбранная валюта:', code)
  dropVisible.value = false
}

function onButtonClicked(code, index) {
  lastClickedIndex.value = index
  activeButton.value = index
  emit('currencySelected', {code, index})
}

watch(() => props.selectedCurrency, (newVal) => {
  const idx = props.quickCurrencies.indexOf(newVal)
  activeButton.value = idx >= 0 ? idx :null
}, {immediate: true})

function onInput(event) {
  emit('updateAmount', event.target.value)
}

const rateDisplay = computed(() => {
  const from = props.selectedCurrency;
  const to = props.targetCurrency;

  if (!from || !to || !props.rates[from] || !props.rates[to]) {
    return '-';
  }

  const rate = props.rates[to] / props.rates[from];
  const fromName = currencyNames[from] || from;
  const toName = currencyNames[to] || to;

  return `1 ${fromName} = ${rate.toFixed(2)} ${toName}`
})

const emit = defineEmits (['currencySelected', 'updateAmount'])
</script>

<style lang="scss" scoped>
.convertor__input {
  width: 700px;
  font-size: 2rem;
  box-sizing: border-box;
  color: #C05406;
  .convertor__input--name {
    margin-top: 0;
    margin-bottom: 3.75rem;
  }
}

.convertor__input--currency {
  position: relative;
  display: flex;
  justify-content: start;
  width: 100%;
  .currency--btn {
    border: 1px solid #CDCDCD;
    font-size: 2.25rem;
    padding: 1.1875rem 3.75rem;
    position: relative;
    width: 12.3125rem;
    height: 5.3rem;
    &.active {
      background-color: #C05406;
    }
  }
  .currency--array {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid #CDCDCD;
    width: 8.875rem;
    position: relative;
  }
}

.convertor__block--input {
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: #F1F1F1;
  margin-top: 2rem;

  .input__p {
    font-size: 1.5rem;
    color: black;
    margin: 0;
    padding: 2.4rem 0.9rem ;
  }

  .input__input {
    font-size: 6.25rem;
    border: none;
    background-color: #F1F1F1;
    &::-webkit-inner-spin-button,
    &::-webkit-outer-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }
  }
}
</style>