<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Crypto Prices</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-button expand="full" @click="fetchData">Refresh</ion-button>
      <ion-grid>
        <ion-row class="header-row">
          <ion-col>Rank</ion-col>
          <ion-col>Bitcoin</ion-col>
          <ion-col>USD</ion-col>
        </ion-row>
        <ion-row v-for="crypto in cryptocurrencies" :key="crypto.id" class="data-row">
          <ion-col>{{ crypto.rank }}</ion-col>
          <ion-col>{{ crypto.name }} ({{ crypto.symbol }})</ion-col>
          <ion-col>${{ crypto.price_usd }}</ion-col>
        </ion-row>
      </ion-grid>
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
.header-row {
  background-color: #fdd79a;
  font-weight: bold;
  text-align: center;
}

.data-row {
  text-align: center;
}

ion-col {
  border: 1px solid #ddd;
  padding: 8px;
}

ion-button {
  margin: 10px;
}
</style>
