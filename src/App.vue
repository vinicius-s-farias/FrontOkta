<template>
  <div id="app" class="bg-gray-200">
    <div>
      <!-- COMEÇO DO MENU SUPERIOR -->
      <nav
        class="relative flex flex-wrap items-center justify-between px-2 py-4 bg-gray-800 mb-3"
        aria-label="mydesc"
      >
        <div
          class="container px-4 mx-auto flex flex-wrap items-center justify-between"
        >
          <div
            class="w-full relative lg:w-auto px-4 lg:static lg:block lg:justify-start"
          >
            <div class="flex justify-between">
              <img
                width="30"
                src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT9Q_TOF8rxhZ5B6ELRNM-W2pOGHXAVdD3RDg&usqp=CAU"
                alt=""
              />
              <a
                class="text-base font-bold leading-relaxed inline-block mr-4 py-2 whitespace-nowrap uppercase text-white no-underline ml-2"
              >
                Solin-Vest
              </a>
            </div>
            <button
              class="cursor-pointer text-xl leading-none px-3 py-1 border border-solid border-transparent rounded bg-transparent block lg:hidden outline-none focus:outline-none"
              type="button"
            >
              <span class="block relative w-6 h-px rounded-sm bg-white"></span>
              <span
                class="block relative w-6 h-px rounded-sm bg-white mt-1"
              ></span>
              <span
                class="block relative w-6 h-px rounded-sm bg-white mt-1"
              ></span>
            </button>
          </div>
          <div
            class="lg:flex flex-grow items-center"
            id="example-navbar-warning"
          >
            <ul class="flex flex-col lg:flex-row list-none ml-auto">
              <li class="nav-item">
                <a
                  class="px-3 py-2 flex items-center uppercase font-bold text-white hover:opacity-75"
                >
                  <router-link to="/login" v-if="!authenticated">
                    Login
                  </router-link>
                </a>
              </li>
              <div class="flex justify-between">
                <img
                  width="30"
                  src="https://img1.gratispng.com/20180319/fvw/kisspng-computer-icons-user-profile-clip-art-person-icon-user-person-man-icon-5ab04a2bc71e38.6372538715215027638156.jpg"
                  alt=""
                />
                <li class="nav-item">
                  <a
                    class="px-3 py-2 flex items-center uppercase font-bold leading-snug text-white no-underline"
                  >
                    {{ nameUs }}
                  </a>
                </li>
              </div>
            </ul>
          </div>
        </div>
      </nav>
    </div>

    <!-- COMEÇO MENU HORIZONTAL -->
    <div class="flex justify-between">
      <nav
        class="navbar w-64 overflow-x-scroll bg-gray-800 top-20"
        style="height: 45em"
        aria-label="mydesc"
      >
        <div class="flex pr-2 justify-center">
          <button @click="tog()" class="p-2"></button>
        </div>

        <ul class="flex flex-col py-4">
          <li>
            <a
              class="no-underline text- flex flex-row items-center h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
            >
              <span
                class="inline-flex items-center justify-center h-12 w-12 text-lg text-gray-400"
                ><em class="bx bx-home"></em
              ></span>

              <span class="text-sm font-medium text-white"></span>
              <router-link
                to="/"
                class="px-3 py-2 flex items-center uppercase font-bold leading-snug text-white hover:opacity-75"
                >Dashboard</router-link
              >
            </a>
          </li>
          <li class="mt-5">
            <button type="button" v-on:click="toggleGrafico()">
              <a
                class="flex flex-row items-center h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
              >
                <span
                  class="inline-flex items-center justify-center h-12 w-12 text-lg text-gray-400"
                  ><em class="bx bx-user"></em
                ></span>
                <span
                  class="px-3 py-2 flex items-center uppercase font-bold leading-snug text-white hover:opacity-75"
                >
                  GRAFICO
                </span>
              </a>
            </button>
          </li>
          <li class="mt-5">
            <button type="button" v-on:click="toggleCarteira()">
              <a
                class="flex flex-row items-center h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
              >
                <span
                  class="inline-flex items-center justify-center h-12 w-12 text-lg text-gray-400"
                  ><em class="bx bx-user"></em
                ></span>
                <span
                  class="px-3 py-2 flex items-center uppercase font-bold leading-snug text-white hover:opacity-75"
                  >Carteira</span
                >
              </a>
            </button>
          </li>
          <button type="button" v-on:click="toggleOrdem()">
            <li class="mt-5">
              <a
                class="flex flex-row items-center h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
              >
                <span
                  class="inline-flex items-center justify-center h-12 w-12 text-lg text-gray-400"
                  ><em class="bx bx-user"></em
                ></span>
                <span
                  class="px-3 py-2 flex items-center uppercase font-bold leading-snug text-white hover:opacity-75"
                  >COMPRA/VENDA</span
                >
              </a>
            </li>
          </button>
          <li class="mt-72">
            <a
              v-if="authenticated"
              v-on:click="logout()"
              @click="this.showGrafico = false"
              class="flex flex-row items-end h-12 transform hover:translate-x-2 transition-transform ease-in duration-200 text-gray-500 hover:text-gray-800"
            >
              <span
                class="inline-flex items-end justify-end h-12 w-12 text-lg text-gray-400"
                ><em class="bx bx-log-out"></em
              ></span>
              <span
                class="px-3 py-2 flex items-center uppercase font-bold leading-snug text-white hover:opacity-75 mt-48"
                >Logout</span
              >
            </a>
          </li>
        </ul>
      </nav>

      <div id="content" class="w-11/12">
        <router-view />
      </div>
    </div>

    <!-- COMEÇO MODAL CARTEIRA -->
    <div class="w-1/12">
      <div
        v-if="showCarteira"
        class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex"
      >
        <div class="relative w-auto my-6 mx-auto max-w-6xl">
          <!--content-->
          <div
            class="border-0 rounded-lg shadow-lg relative flex flex-col w-full bg-white outline-none focus:outline-none"
          >
            <!--header-->
            <div
              class="flex items-start justify-center p-1 border-b border-solid border-blueGray-200 rounded-t"
            >
              <h5 class="text-3xl font-semibold">Carteira</h5>
            </div>
            <!--body-->
            <table class="divide-gray-200 w-full">
              <caption></caption>
              <thead class="bg-gray-500">
                <tr>
                  <th
                    scope="col"
                    class="px-20 py-3 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
                  >
                    Ação
                  </th>
                  <th
                    scope="col"
                    class="px-20 py-3 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
                  >
                    Simbolo
                  </th>
                  <th
                    scope="col"
                    class="px-20 py-3 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
                  >
                    Volume
                  </th>
                </tr>
              </thead>
              <tbody class="bg-gray-100 divide-y divide-gray-200">
                <tr v-for="wallets in wallet" :key="wallets">
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="flex items-center">
                      <div class="ml-4">
                        <div class="text-sm font-medium text-gray-900">
                          {{ wallets.stockName }}
                        </div>
                      </div>
                    </div>
                  </td>
                  <td class="px-20 py-4 whitespace-nowrap">
                    <div class="text-sm text-gray-900">
                      {{ wallets.stockSymbol }}
                    </div>
                  </td>
                  <td class="px-20 py-4 whitespace-nowrap">
                    {{ wallets.volume }}
                  </td>
                </tr>
              </tbody>
            </table>

            <!--footer-->
            <div
              class="flex items-center justify-between p-3 border-t border-solid border-blueGray-200 rounded-b"
            >
              <h1 class="text-xl font-semibold">Patrimonio :</h1>
              <h1>{{ dollar }}</h1>
              <button
                class="py-3 px-8 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-red-300 hover:bg-gray-200 focus:outline-none"
                type="button"
                v-on:click="toggleCarteira()"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
      <div
        v-if="showCarteira"
        class="opacity-25 fixed inset-0 z-40 bg-black"
      ></div>
    </div>

    <!-- COMEÇO MODAL GRAFICO -->
    <div class="w-1/2">
      <div
        v-if="showGrafico"
        class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex"
      >
        <div class="relative w-1/2 my-6 mx-auto max-w-6xl">
          <!--content-->
          <div
            class="border-0 rounded-lg shadow-lg relative flex flex-col w-full bg-white outline-none focus:outline-none"
          >
            <!--header-->
            <div
              class="flex items-start justify-center p-1 border-b border-solid border-blueGray-200 rounded-t"
            >
              <h5 class="text-3xl font-semibold">SELECIONE SUA AÇÃO</h5>
            </div>
            <!--body-->

            <div class="w-full md:max-w-full mb-6 md:mb-0 pb-3 p-2">
              <div>
                <label
                  class="justify-center block text-sm font-medium text-gray-700"
                >
                </label>
                <select
                  v-model="name"
                  class="mt-1 mb- block w-full py-2 px-3 border bg-gray-200 border-gray-200 text-gray-700 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                >
                  <option v-for="stocks in seila" :key="stocks">
                    {{ stocks.stockName }}
                  </option>
                </select>
              </div>
            </div>

            <div
              id="chart-demo "
              class="bg-green-50 mx-4 w-auto"
              v-if="ShowCard"
            >
              <DxChart
                id="zoomedChart"
                :data-source="dataSource"
                class="text-3xl font-semibold"
                :title="this.stocks2[0].stockName + ' PRICES'"
              >
                <DxSeries
                  type="candlestick"
                  open-value-field="open"
                  high-value-field="max"
                  low-value-field="min"
                  close-value-field="close"
                  argument-field="created_on"
                >
                  <DxAggregation :enabled="true" />
                </DxSeries>
                <DxArgumentAxis
                  :visual-range="visualRange"
                  :value-margins-enabled="false"
                  argument-type="datetime"
                >
                  <DxGrid :visible="true" />
                  <DxLabel :visible="false" />
                </DxArgumentAxis>
                <DxValueAxis value-type="numeric" />
                <DxMargin :right="10" />
                <DxLegend :visible="false" />
                <DxTooltip :enabled="true" />
              </DxChart>
              <DxRangeSelector
                :data-source="dataSource"
                v-model:value="visualRange"
              >
                <DxSize :height="120" />
                <DxRsChart>
                  <DxRsValueAxis value-type="numeric" />
                  <DxRsSeries
                    type="line"
                    value-field="open"
                    argument-field="created_on"
                    class="bg-gray-300"
                  >
                    <DxRsAggregation :enabled="true" />
                  </DxRsSeries>
                </DxRsChart>
                <DxScale
                  :placeholder-height="20"
                  minor-tick-interval="day"
                  tick-interval="month"
                  value-type="datetime"
                  aggregation-interval="week"
                />
                <DxBehavior
                  :snap-to-ticks="false"
                  call-value-changed="onMoving"
                />
              </DxRangeSelector>
            </div>
            <!--footer-->
            <div
              class="flex items-center justify-between p-3 border-t border-solid border-blueGray-200 rounded-b"
            >
              <button
                class="py-3 px-8 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-green-300 hover:bg-gray-200 focus:outline-none"
                @click="Grafico"
              >
                PRUCURAR
              </button>
              <button
                class="py-3 px-8 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-red-300 hover:bg-gray-200 focus:outline-none"
                type="button"
                v-on:click="toggleGrafico()"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
      <div
        v-if="showGrafico"
        class="opacity-25 fixed inset-0 z-40 bg-black"
      ></div>
    </div>

    <!-- COMEÇO MODAL ORDEM -->
    <div class="w-1/12">
      <div
        v-if="showOrdem"
        class="overflow-x-hidden overflow-y-auto fixed inset-0 z-50 outline-none focus:outline-none justify-center items-center flex"
      >
        <div class="relative w-auto my-6 mx-auto max-w-6xl">
          <!--content-->
          <div
            class="border-0 rounded-lg shadow-lg relative flex flex-col w-full bg-white outline-none focus:outline-none"
          >
            <!--header-->
            <div
              class="flex items-start justify-center p-1 border-b border-solid border-blueGray-200 rounded-t"
            >
              <h5 class="text-3xl font-semibold">CRIE SUA ORDEM</h5>
            </div>
            <!--body-->
            <form class="w-full max-w-lg p-3">
              <div class="w-full md:min-w-full mb-6 md:mb-0 pb-3">
                <div class="col-span-6">
                  <label
                    class="justify-center block text-sm font-medium text-gray-700"
                    >Ação
                  </label>
                  <select
                    @click="setup"
                    v-model="name"
                    class="mt-1 mb- block w-full py-2 px-3 border bg-gray-200 border-gray-200 text-gray-700 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                  >
                    <option v-for="stock in seila" :key="stock">
                      {{ stock.stockName }}
                    </option>
                  </select>
                </div>
              </div>

              <div class="flex justify-evenly -mx-3 mb-2">
                <div class="w-1/2 md:w-1/3 px-3 mb-6 md:mb-0">
                  <label
                    class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    for="grid-state"
                  >
                    Tipo
                  </label>
                  <div class="relative">
                    <select
                      v-model="type"
                      class="block appearance-none bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                    >
                      <option value="1">Venda</option>
                      <option value="0">Compra</option>
                    </select>
                    <div
                      class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
                    ></div>
                  </div>
                </div>

                <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
                  <label
                    class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    for="grid-city"
                  >
                    Quantidade
                  </label>
                  <input
                    v-model="volume"
                    class="appearance-none block w-10/12 bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                    type="text"
                  />
                </div>
                <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
                  <label
                    class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                    for="grid-zip"
                  >
                    Preço
                  </label>
                  <input
                    v-model="price"
                    class="appearance-none block w-10/12 bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                    type="text"
                  />
                </div>
              </div>
            </form>
            <!--footer-->
            <div
              class="flex items-center justify-between p-3 border-t border-solid border-blueGray-200 rounded-b"
            >
              <button
                class="py-3 px-8 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-green-300 hover:bg-gray-200 focus:outline-none"
                @click="CreteOrdem"
              >
                Salvar Ordem
              </button>
              <button
                class="py-3 px-8 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-red-300 hover:bg-gray-200 focus:outline-none"
                type="button"
                v-on:click="toggleOrdem()"
              >
                Close
              </button>
            </div>
          </div>
          <div
            v-if="falhou"
            class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative"
            role="alert"
          >
            <span class="block sm:inline">Ordem Não Criada</span>
            <span class="absolute top-0 bottom-0 right-0 px-4 py-3">
              <svg
                class="fill-current h-6 w-6 text-red-500"
                role="button"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <title>Close</title>
                <path
                  d="M14.348 14.849a1.2 1.2 0 0 1-1.697 0L10 11.819l-2.651 3.029a1.2 1.2 0 1 1-1.697-1.697l2.758-3.15-2.759-3.152a1.2 1.2 0 1 1 1.697-1.697L10 8.183l2.651-3.031a1.2 1.2 0 1 1 1.697 1.697l-2.758 3.152 2.758 3.15a1.2 1.2 0 0 1 0 1.698z"
                />
              </svg>
            </span>
          </div>
          <div
            v-if="sucesso"
            class="bg-green-100 border border-green-400 text-black px-4 py-3 rounded relative"
            role="alert"
          >
            <span class="block sm:inline">Ordem Criada com sucesso</span>
            <span class="absolute top-0 bottom-0 right-0 px-4 py-3">
              <svg
                class="fill-current h-6 w-6 text-gre"
                role="button"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <title>Close</title>
                <path
                  d="M14.348 14.849a1.2 1.2 0 0 1-1.697 0L10 11.819l-2.651 3.029a1.2 1.2 0 1 1-1.697-1.697l2.758-3.15-2.759-3.152a1.2 1.2 0 1 1 1.697-1.697L10 8.183l2.651-3.031a1.2 1.2 0 1 1 1.697 1.697l-2.758 3.152 2.758 3.15a1.2 1.2 0 0 1 0 1.698z"
                />
              </svg>
            </span>
          </div>
        </div>
      </div>
      <div
        v-if="showModal"
        class="opacity-25 fixed inset-0 z-40 bg-black"
      ></div>
    </div>

    <!-- COMEÇO FOOTER -->
    <div>
      <footer
        class="bg-gray-800 shadow md:p-6 dark:bg-gray-800 fixed inset-x-0 bottom-0 md:text-center text-white"
      >
        © 2022 Solin-Vest.
      </footer>
    </div>
  </div>
</template>

<script>
import "./assets/tailwind.css";
import axios from "axios";
import DxChart, {
  DxSeries,
  DxAggregation,
  DxArgumentAxis,
  DxGrid,
  DxLabel,
  DxValueAxis,
  DxMargin,
  DxLegend,
  DxTooltip,
} from "devextreme-vue/chart";

import DxRangeSelector, {
  DxSize,
  DxScale,
  DxChart as DxRsChart,
  DxValueAxis as DxRsValueAxis,
  DxSeries as DxRsSeries,
  DxAggregation as DxRsAggregation,
  DxBehavior,
} from "devextreme-vue/range-selector";

export default {
  components: {
    DxChart,
    DxSeries,
    DxAggregation,
    DxArgumentAxis,
    DxGrid,
    DxLabel,
    DxValueAxis,
    DxMargin,
    DxLegend,
    DxTooltip,
    DxRangeSelector,
    DxSize,
    DxScale,
    DxRsChart,
    DxRsValueAxis,
    DxRsSeries,
    DxRsAggregation,
    DxBehavior,
  },

  name: "app",
  data: function () {
    return {
      sucesso: false,
      falhou: false,
      authenticated: false,
      open: true,
      showOrdem: false,
      showCarteira: false,
      showGrafico: false,
      ShowCard: false,
      wallet: [],
      id_user: 0,
      users: [],
      nameUs: "",
      dollar: "",
      us: [],
      user: "",
      stock: [],
      name: "",
      seila: [],
      seila1: [],
      stocks: [],
      stocks2: [],
      dataSource: [],
      visualRange: [],
    };
  },

  created() {
    this.User();
    this.UserID();
  },
  async created1() {
    await this.isAuthenticated();
    this.$auth.authStateManager.subscribe(this.isAuthenticated);
  },
  watch: {
    // Everytime the route changes, check for auth status
    $route: "isAuthenticated",
  },
  methods: {
    async isAuthenticated() {
      this.authenticated = await this.$auth.isAuthenticated();
    },
    async logout() {
      await this.$auth.signOut();
    },
    toggle() {
      this.open = !this.open;
    },
    tog() {
      this.open = !this.open;
    },
    toggleCarteira() {
      this.showCarteira = !this.showCarteira;
      this.Carteira1();
    },

    toggleGrafico() {
      this.showGrafico = !this.showGrafico;
      this.setup().then(() => {
        this.name = "";
      });
    },

    toggleOrdem() {
      this.showOrdem = !this.showOrdem;
      this.setup();
    },

    async User() {
      this.claims = await Object.entries(await this.$auth.getUser()).map(
        (entry) => ({ claim: entry[0], value: entry[1] })
      );
      let accessToken = this.$auth.getAccessToken();
      console.log(accessToken);
      try {
        let response = await axios.get(
          `http://localhost:8081/users/${this.claims[1].value}`,

          {
            headers: { Authorization: "Bearer " + accessToken },
          }
        );
        console.log(response.data);
        this.id_user = response.data;
        console.log("olha pra baixo");
      } catch (error) {
        this.id_user = `${error}`;
      }
    },

    async Carteira1() {
      if (this.$root.authenticated) {
        this.claims = await this.$auth.getUser();
        let accessToken = this.$auth.getAccessToken();
        console.log(`Authorization: Bearer ${accessToken}`);
        try {
          let response = await axios.get(
            `http://localhost:8081/wallet/${this.id_user}`,
            {
              headers: { Authorization: "Bearer " + accessToken },
            }
          );
          this.wallet = response.data;
        } catch (error) {
          this.wallet = `${error}`;
        }
      }
    },

    async UserID() {
      this.claims = await Object.entries(await this.$auth.getUser()).map(
        (entry) => ({ claim: entry[0], value: entry[1] })
      );
      let accessToken = this.$auth.getAccessToken();
      try {
        let response = await axios.get(
          `http://localhost:8081/teste/${this.id_user}`,

          {
            headers: { Authorization: "Bearer " + accessToken },
          }
        );
        console.log(response.data);
        this.us = response.data;
        this.dollar = this.us[0].dollarBalance.toLocaleString("pt-br", {
          style: "currency",
          currency: "BRL",
        });
        this.nameUs = this.us[0].username;
      } catch (error) {
        this.us = `${error}`;
      }
    },

    async CreteOrdem() {
      if (this.$root.authenticated) {
        this.claims = await this.$auth.getUser();
        let accessToken = this.$auth.getAccessToken();
        try {
          await axios
            .post(
              "http://localhost:8081/order",
              {
                idUser: this.id_user,
                idStock: this.seila1[0].id,
                stockName: this.name,
                stockSymbol: this.seila1[0].stockSymbol,
                price: this.price,
                status: 1,
                type: this.type,
                volume: this.volume,
                remainingValue: this.volume,
              },
              {
                headers: { Authorization: "Bearer " + accessToken },
              }
            )
            .then(() => {
              this.sucesso = true;
              this.falhou = false;
              this.name = "";
              this.price = "";
              this.volume = "";
              this.type = "";
            });
        } catch (error) {
          console.log(error);
          this.falhou = true;
          this.sucesso = false;
        }
      }

      this.setup2();
    },

    async Grafico() {
      this.claims = await this.$auth.getUser();
      let accessToken = this.$auth.getAccessToken();
      console.log(`Authorization: Bearer ${accessToken}`);
      try {
        let response = await axios.get(
          `http://localhost:8082/stocks/${this.name}`,

          {
            headers: { Authorization: "Bearer " + accessToken },
          }
        );
        this.stocks2 = response.data;
      } catch (error) {
        this.stocks2 = `${error}`;
      }
      try {
        let response = await axios.get(
          `http://localhost:8082/grafico/${this.stocks2[0].id}`,
          {
            headers: { Authorization: "Bearer " + accessToken },
          }
        );

        this.dataSource = response.data;
        console.log(this.dataSource);
      } catch (error) {
        this.dataSource = `${error}`;
      }
      this.ShowCard = true;
    },

    async setup() {
      this.claims = await this.$auth.getUser();
      let accessToken = this.$auth.getAccessToken();
      console.log(`Authorization: Bearer ${accessToken}`);
      try {
        let response = await axios.get("http://localhost:8082/stocks/all", {
          headers: { Authorization: "Bearer " + accessToken },
        });

        this.seila = response.data;
      } catch (error) {
        this.seila = `${error}`;
      }

      try {
        let response = await axios.get(
          `http://localhost:8082/stocks/${this.name}`,

          {
            headers: { Authorization: "Bearer " + accessToken },
          }
        );
        this.seila1 = response.data;
      } catch (error) {
        this.seila1 = `${error}`;
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
  },
};
</script>

<style>
nav div a {
  margin-right: 30px;
}
#app {
  width: 1900px;
  margin: 0 auto;
}
a {
  text-decoration: underline;
  cursor: pointer;
}
.navbar {
  transition: all 330ms ease-out;
}

.navbar-open {
  transform: translateX(0%);
}
.navbar-close {
  transform: translateX(-100%);
}
</style>
