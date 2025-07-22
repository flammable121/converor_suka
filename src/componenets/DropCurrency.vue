<template>
<div class="drop">
    <div class="drop__window">
        <ul class="drop__window--ul">
            <li 
                v-for="[code] in currencies"
                :key="code"
                class="drop__window--li"
            > 
                {{ code }}
            </li>
        </ul>
    </div>
</div>
</template>

<script setup>
defineProps({
    currencies: {
        type: Array,
        required: true
    },
    loadingCurrency: {
        type: Boolean,
        required: true
    }
});
</script>

<style lang="scss" scoped>
.drop {
    overflow: auto;
    z-index: 1000;
    position: absolute;
    width: 100%;
    height: 65.1%;
    bottom: -8rem;

    &::-webkit-scrollbar {
        display: none;
    }

    .drop__window--ul {
        background-color: #ffff;
        columns: 8; 
    }

    .drop__window--li {
        text-align: center;
        list-style: none;
        font-size: 1.5rem;
        overflow: auto;
        cursor: pointer;
        margin: 1.6rem auto;
    }
}


</style>