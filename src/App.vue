<template>
    <div class="converter">
        <h3 class="converter__title">Конвертер валют</h3>
        <div class="converter__box">
            <currency-input></currency-input>
            <div class="converter_array">
                <svg xmlns="http://www.w3.org/2000/svg" width="70" height="88" viewBox="0 0 70 88" fill="none">
                    <path d="M23.6443 48.4825L45.6784 26.4483C46.0689 26.0578 46.069 25.4247 45.6784 25.0341L23.6443 2.99999" stroke="black" stroke-width="4" stroke-linecap="square"/>
                    <path d="M46.5707 39.6822L24.5365 61.7163C24.146 62.1069 24.146 62.74 24.5365 63.1305L46.5707 85.1647" stroke="black" stroke-width="4" stroke-linecap="square"/>
                </svg>
            </div>
            <currency-input></currency-input>
        </div>
    </div>    
</template>

<script setup>
import CurrencyInput from './componenets/CurrencyInput.vue';

</script>

<style lang="scss">
body {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.converter {
    & h3 {
        
        font-size: 64px;
    }

}
.converter_array {

}
.converter__box {
    display: flex;
    align-items: center;

}

@media (max-width: 800px) {

}

</style>