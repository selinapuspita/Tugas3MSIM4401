<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Crypto App</ion-title>
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
        <ion-row v-for="crypto in cryptocrruencies" :key="crypto.id" class="data-row">
          <ion-col>{{ crypto.rank }}</ion-col>
          <ion-col>{{ crypto.name }} ({{ crypto.symbol }})</ion-col>
          <ion-col>{{ crypto.price_usd }}</ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
  import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
</script>

<style scoped>
  #container {
    text-align: center;

    position: absolute;
    left: 0;
    right: 0;
    top: 50%;
    transform: translateY(-50%);
  }

  #container strong {
    font-size: 20px;
    line-height: 26px;
  }

  #container p {
    font-size: 16px;
    line-height: 22px;

    color: #8c8c8c;

    margin: 0;
  }

  #container a {
    text-decoration: none;
  }
</style>