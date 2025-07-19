<template>
<div class="convertor__input">
    <p class="convertor__input--name">Хочу приобрести</p>
        <div class="convertor__input--currency">
            <button class="currency--btn">USD</button>
            <button class="currency--btn">USD</button>
            <button class="currency--btn">USD</button>
            <span 
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
</div>
</template>

<script setup>



</script>

<style lang="scss" scoped>
.convertor__input {
    width: 733px;
    margin: 50px;
    & {
        font-size: 36px;
        color: #C05406;
    }

}

.convertor__input--currency {
    display: flex;

    & button, span {
    border: 1px solid #CDCDCD;
    font-size: 36px;
    padding: 29px 60px;
    position: relative;
    &:focus {
        background-color: #C05406;
    }
}
}


.convertor__block--input {
    display: flex;
    flex-direction: column;
    & p {
        font-size: 24px;
        color: black;
    }
    & input {
        font-size: 100px;
        border: none;
    }
}

.input__currency {
    font-size: 24px;
}

</style>