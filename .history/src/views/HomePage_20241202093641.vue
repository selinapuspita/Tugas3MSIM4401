<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Crypto Prices</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-button expand="full" @click="fetchData">Refresh</ion-button>
      <ion-list>
        <ion-item v-for="crypto in cryptocurrencies" :key="crypto.id">
          <ion-label>
            <h2>Rank {{ crypto.rank }}: {{ crypto.name }} ({{ crypto.symbol }})</h2>
            <p>Price: ${{ crypto.price_usd }}</p>
          </ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      cryptocurrencies: [],
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('https://api.coinlore.net/api/tickers/');
        this.cryptocurrencies = response.data.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style scoped>
ion-item {
  background-color: #fdf5e6;
  margin: 5px 0;
  border-radius: 8px;
}
ion-button {
  margin: 10px;
}
</style>
