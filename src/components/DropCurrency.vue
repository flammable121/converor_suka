<template>
<div class="drop">
    <div class="drop__window">
        <ul class="drop__window--ul">
            <li 
                @click="$emit('currencySelected', code)"
                v-for="code in currencies"
                :key="code"
                class="drop__window--li"
            > 
                {{ code }} : {{ currencyNames[code] || code }}
            </li>
        </ul>
    </div>
</div>
</template>

<script setup>
import { currencyNames } from '@/cyrrencyNames';

defineProps({
    currencies: {
        type: Array,
        required: true
    },
});

defineEmits(['currencySelected'])
</script>

<style lang="scss" scoped>
.drop {
    color: black;
    overflow: auto;
    z-index: 1000;
    position: absolute;
    height: 350px;
    &::-webkit-scrollbar {
        display: none;
    }

    .drop__window--ul {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        text-align: left;
        background-color: #F1F1F1; 
    }

    .drop__window--li {
        list-style: none;
        font-size: 18px;
        overflow: auto;
        cursor: pointer;
        margin: auto;
        width: calc(30%);
    }
}


</style>