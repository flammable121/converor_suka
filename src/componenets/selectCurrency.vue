<!-- <template>
    <div>
        <select>
            <option  v-for="currency in currencies" :key="currency">
                {{ currency }}              
            </option>
        </select>
    </div>
</template>

<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

const rates = ref('')
const currencies = ref ([])

onMounted(async() => {
    const response = await axios.get('https://api.currencyfreaks.com/v2.0/rates/latest?apikey=a9e13e0f86234e5caa2e8a0dad0d2a66')

    rates.value = response.data.rates
    currencies.value = Object.keys(rates.value)

});
</script>

<style  scoped>
select {
    padding: 16px 30px;
    font-size: 36px;
    border: none;
    appearance: none;
    text-align: center;

}
</style> -->