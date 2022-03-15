<template>
  <!-- COMEÇO Do STOCK -->

  <div class="pt-40 pb-3 flex w-full md:w-auto p-2">
    <div class="bg-gray-300 rounded-lg shadow-2x1 w-full -mt-40">
      <!-- header -->

      <header
        class="flex justify-between bg-gray-800 rounded-t-lg py-1 px-8 text-xl font-normal text-white"
      >
        ULTIMAS COTAÇÕES

        <ul>
          <a
            class="no-underline text- flex flex-row items-center h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
          >
            <router-link
              to="/About"
              class="flex items-center uppercase font-bold leading-snug text-white hover:opacity-50 no-underline"
            >
              Ver Todas</router-link
            >
          </a>
        </ul>
      </header>

      <table class="min-w-full divide-y divide-gray-200">
        <caption></caption>
        <thead class="bg-gray-500">
          <tr>
            <th
              scope="col"
              class="px-20 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ação
            </th>
            <th
              scope="col"
              class="px-20 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Simbolo
            </th>
            <th
              scope="col"
              class="px-20 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ask-Min
            </th>
            <th
              scope="col"
              class="px-20 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ask-Max
            </th>
            <th
              scope="col"
              class="px-20 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              BID-MIN
            </th>
            <th
              scope="col"
              class="px-20 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              BID-MAX
            </th>
          </tr>
        </thead>
        <tbody class="bg-gray-100 divide-y divide-gray-200">
          <tr v-for="stock in stocks" :key="stock">
            <td class="px-6 py-0 whitespace-nowrap">
              <div class="flex items-center">
                <div class="flex-shrink-0 h-10 w-10"></div>
                <div class="ml-4">
                  <div class="text-sm font-medium text-gray-900">
                    {{ stock.stockName }}
                  </div>
                </div>
              </div>
            </td>
            <td class="px-20 py-0 whitespace-nowrap">
              <div class="text-sm text-gray-900">{{ stock.stockSymbol }}</div>
            </td>
            <td class="px-20 py-0 whitespace-nowrap">
              {{
                stock.askMin.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-20 py-0 whitespace-nowrap text-sm text-gray-900">
              {{
                stock.askMax.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-20 py-0 whitespace-nowrap text-sm text-gray-900">
              {{
                stock.bidMin.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-20 py-0 whitespace-nowrap text-sm text-gray-900">
              {{
                stock.bidMax.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <!-- COMEÇO DA ORDEM -->

  <div class="flex w-full md:w-auto p-2">
    <div class="bg-gray-100 rounded-lg shadow-2x1 w-full">
      <header
        class="flex justify-between bg-gray-800 rounded-t-lg py-2 px-8 text-xl font-extrabold text-white"
      >
        COMPRAS E VENDAS
        <ul>
          <a
            class="no-underline text- flex flex-row items-center h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
          >
            <router-link
              to="/Profile"
              class="flex items-center uppercase font-bold leading-snug text-white hover:opacity-50 no-underline"
            >
              Ver Todas</router-link
            >
          </a>
        </ul>
      </header>
      <table class="min-w-full divide-y divide-gray-200">
        <caption></caption>
        <thead class="bg-gray-500">
          <tr>
            <th
              scope="col"
              class="px-16 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ação
            </th>
            <th
              scope="col"
              class="px-16 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Simbolo
            </th>
            <th
              scope="col"
              class="px-14 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Tipo
            </th>
            <th
              scope="col"
              class="px-16 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Preço
            </th>
            <th
              scope="col"
              class="px-16 py-2 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Volume
            </th>
          </tr>
        </thead>
        <tbody class="bg-gray-100 divide-y divide-gray-200">
          <tr v-for="orders in order" :key="orders">
            <td class="py-4 whitespace-nowrap">
              <div class="flex items-center">
                <div class="flex-shrink-0 h-10 w-10"></div>
                <div class="ml-4">
                  <div class="text-sm font-medium text-gray-900">
                    {{ orders.stockName }}
                  </div>
                </div>
              </div>
            </td>
            <td class="px-16 py-1 whitespace-nowrap">
              <div class="text-sm text-gray-900">{{ orders.stockSymbol }}</div>
            </td>
            <td class="px-14 py-1 whitespace-nowrap" v-if="orders.type == 1">
              Venda
            </td>
            <td class="px-14 py-1 whitespace-nowrap" v-else>Compra</td>
            <td class="px-16 p y-1 whitespace-nowrap">
              {{
                orders.price.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-16 py-1 whitespace-nowrap">
              {{ orders.remainingValue }}
            </td>
          </tr>
        </tbody>
      </table>

      <div class="p-0"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { fetchEventSource } from "@microsoft/fetch-event-source";

export default {
  name: "home",
  nome: "large-modal",
  data: function () {
    return {
      id_user: 0,

      users: [],
      seila: [],

      price: "",
      volume: "",
      type: "",
      name: "",
      username: "",
      showModal: false,
      claims: "",
      stocks: [],
      order: [],
      dataSource: [],
      visualRange: [],
      sucesso: false,
    };
  },

  created() {
    this.setup();
    this.setup2();
    this.Retorno();
  },
  methods: {
    async setup() {
      this.claims = await this.$auth.getUser();
      let accessToken = this.$auth.getAccessToken();
      console.log(`Authorization: Bearer ${accessToken}`);
      try {
        let response = await axios.get("http://localhost:8082/stocks", {
          headers: { Authorization: "Bearer " + accessToken },
        });
        this.stocks = response.data;
      } catch (error) {
        this.stocks = `${error}`;
      }
    },
    async setup2() {
      this.claims = await this.$auth.getUser();
      let accessToken = this.$auth.getAccessToken();
      console.log(`Authorization: Bearer ${accessToken}`);
      try {
        let response = await axios.get("http://localhost:8081/orders", {
          headers: { Authorization: "Bearer " + accessToken },
        });
        this.order = response.data;
      } catch (error) {
        this.order = `${error}`;
      }
    },

    async Retorno() {
      let accessToken = this.$auth.getAccessToken();
      console.log("to entrando");
      const PauloTeste = (teste) => {
        this.stocks = teste;
      };
      await fetchEventSource("http://localhost:8082/stocks/subscribe", {
        headers: {
          Authorization: "Bearer " + accessToken,
        },
        onmessage(ev) {
          PauloTeste(JSON.parse(ev.data));
        },
        onerror(err) {
          if (err) {
            console.log("Sou do erro", err);
            throw err; // rethrow to stop the operation
          }
        },
      });
    },

    toggleModal: function () {
      this.showModal = !this.showModal;
    },
  },
};
</script>
