<template>
<div class="convertor__input">
    <p class="convertor__input--name">Хочу приобрести</p>
        <div class="convertor__input--currency">
            <button class="currency--btn">USD</button>
            <button class="currency--btn">USD</button>
            <button class="currency--btn">USD</button>
            <span class="currency--array">
                <svg xmlns="http://www.w3.org/2000/svg" width="52" height="28" viewBox="0 0 52 28" fill="none">
                    <path d="M3.18811 3.00348L25.2222 25.0376C25.6128 25.4281 26.2459 25.4281 26.6365 25.0376L48.6706 3.00348" stroke="#C05406" stroke-width="4" stroke-linecap="square"/>
                </svg>
          </span>
          <drop-currency/>
        </div>
    <div class="convertor__block--input">
        <p class="input__p">Казахстанский тенге</p>
        <input class="input__input" type="number" v-model="amountTo">
        <p class="input__p">1 USD = 468.27 KZT</p>
    </div>
</div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
.convertor__input {
  max-width: 45.875rem;
  font-size: 2.25rem;
  box-sizing: border-box;
  color: #C05406;
  .convertor__input--name {
    margin-top: 0;
    margin-bottom: 3.75rem;
  }
}

.convertor__input--currency {
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
    &:focus {
      background-color: #C05406;
    }
  }
  .currency--array {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid #CDCDCD;
    width: 8.875rem;
  }
}

.convertor__block--input {
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
  }
}
</style>