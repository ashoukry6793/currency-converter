<template>
  <v-app>
    <div id="main">
      <div class="currency-exchange">
        <div class="currency-exchange__convert-from">
          <v-card elevation="2" class="currency-exchange__convert-from__currency">
            <v-select
                v-model="exchangeFromCurrency"
                :items="exchangeFrom"
                item-value="currency"
                item-text="currency"
                hide-details
                flat
                solo>
              <template #selection="{ item }">
                <div class="exchange-currency">
                  <v-img width="50px" class="exchange-currency__flag" :src="item.currencyFlag" />
                  <div class="exchange-currency__name">
                    {{ item.currency }}
                  </div>
                </div>
              </template>
              <template #item="{ item }">
                <div class="exchange-currency">
                  <v-img width="50px" class="exchange-currency__flag" :src="item.currencyFlag" />
                  <div class="exchange-currency__name">
                    {{ item.currency }}
                  </div>
                </div>
              </template>
            </v-select>
          </v-card>
          <v-card rounded elevation="2" class="currency-exchange__convert-from__value">
            <v-text-field v-model="exchangeFromVal" hide-details outlined label="Value">
            </v-text-field>
          </v-card>
          </div>
        <div class="currency-exchange__convert-to">
          <v-card elevation="2" class="currency-exchange__convert-from__currency">
            <v-select
                v-model="exchangeToCurrency"
                :items="exchangeTo"
                item-value="currency"
                item-text="currency"
                hide-details
                flat
                solo>
              <template #selection="{ item }">
                <div class="exchange-currency">
                  <v-img width="50px" class="exchange-currency__flag" :src="item.currencyFlag" />
                  <div class="exchange-currency__name">
                    {{ item.currency }}
                  </div>
                </div>
              </template>
              <template #item="{ item }">
                <div class="exchange-currency">
                  <v-img width="50px" class="exchange-currency__flag" :src="item.currencyFlag" />
                  <div class="exchange-currency__name">
                    {{ item.currency }}
                  </div>
                </div>
              </template>
            </v-select>
          </v-card>
          <v-card rounded elevation="2" class="currency-exchange__convert-from__value">
            <v-text-field readonly :value="exchangeToVal" hide-details outlined label="Value">
            </v-text-field>
          </v-card>
        </div>
        <div class="currency-exchange__meta">
          <div class="currency-exchange__meta__exchange-rate">
            <img class="currency-exchange__meta__exchange-rate__icon" src="./assets/exchange.png">
            <div> {{ exchangeRate }} {{ exchangeToCurrency }} exchange rate</div>
          </div>
        </div>
      </div>
    </div>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  data: () => ({
    exchangeFromVal: 0,
    exchangeFromCurrency: 'USD',
    exchangeToCurrency: 'EUR',
    exchangeFrom: [
      {
        currency: 'USD',
        currencyFlag: './currency-flags/usd.jpg'
      },
      {
        currency: 'EUR',
        currencyFlag: './currency-flags/eur.webp'
      },
      {
        currency: 'CAD',
        currencyFlag: './currency-flags/cad.jpg'
      },
      {
        currency: 'GBP',
        currencyFlag: './currency-flags/uk.jpg'
      },
      {
        currency: 'MXN',
        currencyFlag: './currency-flags/mxn.jpg'
      },
      {
        currency: 'PLN',
        currencyFlag: './currency-flags/pln.png'
      }
    ],
    exchangeTo: [
      {
        currency: 'USD',
        currencyFlag: './currency-flags/usd.jpg'
      },
      {
        currency: 'EUR',
        currencyFlag: './currency-flags/eur.webp'
      },
      {
        currency: 'CAD',
        currencyFlag: './currency-flags/cad.jpg'
      },
      {
        currency: 'GBP',
        currencyFlag: './currency-flags/uk.jpg'
      },
      {
        currency: 'MXN',
        currencyFlag: './currency-flags/mxn.jpg'
      },
      {
        currency: 'PLN',
        currencyFlag: './currency-flags/pln.png'
      }
    ],
    exchangeRates: {
      USD: 1,
      EUR: 0.815894,
      CAD: 1.204355,
      GBP: 0.70602,
      MXN: 19.88162,
      PLN: 3.66121
    }
  }),
  computed: {
    exchangeRate() {
      return this.exchangeRates[this.exchangeToCurrency] / this.exchangeRates[this.exchangeFromCurrency];
    },
    exchangeToVal() {
      return this.exchangeFromVal * this.exchangeRate;
    }
  },
};
</script>
<style lang="scss">
#main {
  $input-height: 100px;
  $input-value-width: 300px;

  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;

  .exchange-currency {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 8px;
    width: 100%;
    row-gap: 4px;

    &__flag {
      border:1px solid #c2c2c2;
      border-radius: 4px;
      width: 50px;
    }

    &__currency {
      text-transform: uppercase;
    }
  }

  .currency-exchange {
    position: relative;
    background-color: #e7fffb;
    height: 300px;
    width: 400px;
    padding-inline-start: 20px;

    &__convert-from {
      position: absolute;
      left: 50%;
      transform: translate(-50%, -10%);
      display: flex;
      flex-direction: row;
      column-gap: 8px;
      width: 500px;

      &__currency {
        padding: 20px 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: $input-height;
      }

      &__value {
        padding: 20px;
        min-width: $input-value-width;
        height: $input-height;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }

    &__convert-to {
      position: absolute;
      bottom: 0;
      left: 50%;
      transform: translate(-50%, 10%);
      display: flex;
      flex-direction: row;
      column-gap: 8px;
      width: 500px;

      &__currency {
        padding: 20px 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: $input-height;
      }

      &__value {
        padding: 20px;
        min-width: $input-value-width;
        height: $input-height;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }

    &__meta {
      height: 100%;
      border-inline-start: 1px dashed blue;
      display: flex;
      justify-content: start;
      align-items: center;

      &__exchange-rate {
        display: flex;
        flex-direction: row;
        transform: translate(-12px, 0);
        column-gap: 8px;

        &__icon {
          height: 24px;
          width: 24px;
          padding: 4px;
          background-color: white;
          border-radius: 50%;
          border: 1px solid blue;
        }
      }
    }
  }
}


</style>
