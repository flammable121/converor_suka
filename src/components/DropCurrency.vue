<template>
<div class="drop">
    <div class="drop__search">
        <input 
            v-model="searchQuery"
            placeholder="Поиск..."
            type="text"
            class="drop__search-input"
        >
    </div>
       <div class="drop__window">
        <ul class="drop__window--ul">
            <li 
                @click="$emit('currencySelected', code)"
                v-for="code in filteredCurrencies"
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
import { ref } from 'vue';
import { currencyNames } from '@/cyrrencyNames';
import { computed } from 'vue';

const props = defineProps({
    currencies: {
        type: Array,
        required: true
    },
});

defineEmits(['currencySelected'])

const searchQuery = ref('')

const filteredCurrencies = computed(() => {
    const query = searchQuery.value.trim().toLowerCase();
    if (!query) return props.currencies;

    return props.currencies.filter(code => {
        const name = currencyNames[code] ? currencyNames[code].toLowerCase() : '';
        return code.toLowerCase().includes(query) || name.includes(query)
    })
})
</script>

<style lang="scss" scoped>
.drop {
    display: flex;
    color: black;
    overflow: auto;
    z-index: 3;
    position: absolute;
    height: 350px;
    &::-webkit-scrollbar {
        display: none;
    }
    .drop__search-input {
        font-size: 2rem;
        width: 100%;
        height: 50px;
        margin: 0;
        padding: 5px;
        position: absolute;
        z-index: 4;
        background-color: #F1F1F1;
        border: 1px solid black;
    }

    .drop__window--ul {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        text-align: left;
        background-color: #F1F1F1; 
        padding-top: 60px;
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