<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="light">

      </ion-toolbar>
    </ion-header>

    <ion-content color="light">
      <div class="container">

        <ion-button expand="block" color="primary" class="refresh-btn" @click="getData">
          Refresh
        </ion-button>

        <ion-list class="list">
          <ion-item v-for="coin in coins" :key="coin.id" class="crypto-card">
            <ion-label>

              <div class="coin-grid">
                <span class="rank-label">Rank</span>
                <span class="name">{{ coin.name }}</span>
                <span class="currency-label">USD</span>

                <span class="rank">{{ coin.rank }}</span>
                <span class="symbol">{{ coin.symbol }}</span>
                <span class="price">{{ coin.price_usd }}</span>
              </div>

            </ion-label>
          </ion-item>
        </ion-list>

      </div>
    </ion-content>
  </ion-page>
</template>

<script setup>
import { ref } from 'vue';
import {
  IonPage, IonHeader, IonToolbar,
  IonContent, IonList, IonItem, IonLabel, IonButton
} from '@ionic/vue';

const coins = ref([]);

async function getData() {
  const response = await fetch("https://api.coinlore.net/api/tickers/");
  const data = await response.json();
  coins.value = data.data;
}

getData();
</script>

<style scoped>
.container {
  background-color: #ffffff;
  min-height: 100vh;
  padding: 16px;
  max-width: 420px;
  /* ukuran mobile */
  margin: 0 auto;
}


.refresh-btn {
  margin-bottom: 20px;
  font-weight: bold;
  border-radius: 8px;
}

.crypto-card {
  background-color: #fff3cd;
  border: 1px solid #d6c98b;
  border-radius: 10px;
  margin: 12px 0;
  padding: 16px;
  color: #d6c98b;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}


.rank-label,
.currency-label {
  font-size: 12px;
  color: #d6c98b;
}

.coin-grid {
  display: grid;
  grid-template-columns: 60px 1fr 120px;
  grid-template-rows: auto auto;
  row-gap: 4px;
  align-items: center;
}

.rank-label,
.rank {
  text-align: left;
}

.name,
.symbol {
  text-align: center;
}

.currency-label,
.price {
  text-align: right;
}

.rank-label,
.currency-label {
  font-size: 12px;
}

.rank,
.symbol,
.price {
  font-size: 20px;
  font-weight: bold;
}
</style>
