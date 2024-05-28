<template>
  <h1>CRYPTO</h1>
  <Input :changeAmount="changeAmount" :convert="convert"/>
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != 0" className="result-text">{{ result }}</p>
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" />
  </div>
</template>

<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
  components: { Input, Selector },
  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0
    }
  },
  methods: {
    changeAmount(val) {
      this.amount = val
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      this.result = 0;

      if (this.amount <= 0) {
        this.error = 'Enter a value greater than 0';
        return;
      } else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
        this.error = 'Choose currencies';
        return;
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = 'Choose different currencies';
        return;
      }

      this.error = '';
      await convert.ready();

      this.result = convert[this.cryptoFirst][this.cryptoSecond](this.amount);
    }
  }
}
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
}
</style>
