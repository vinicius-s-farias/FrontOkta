<template>
  <div class="pt-40 pb-3 flex w-full md:w-auto p-2">
    <div class="bg-gray-300 rounded-lg shadow-2x1 w-full -mt-40">
      <!-- header -->

      <header
        class="flex justify-between bg-gray-800 rounded-t-lg py-1 px-8 text-xl font-normal text-white"
      >
        TODAS AS COTAÇÕES
      </header>

      <table class="min-w-full divide-y divide-gray-200">
        <caption></caption>
        <thead class="bg-gray-500">
          <tr>
            <th
              scope="col"
              class="px-20 py-4 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ação
            </th>
            <th
              scope="col"
              class="px-20 py-4 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Simbolo
            </th>
            <th
              scope="col"
              class="px-20 py-4 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ask-Min
            </th>
            <th
              scope="col"
              class="px-20 py-4 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              Ask-Max
            </th>
            <th
              scope="col"
              class="px-20 py-4 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              BID-MIN
            </th>
            <th
              scope="col"
              class="px-20 py-4 text-left text-xs font-medium text-gray-50 uppercase tracking-wider"
            >
              BID-MAX
            </th>
          </tr>
        </thead>
        <tbody class="bg-gray-100 divide-y divide-gray-200">
          <tr v-for="stock in page.content" :key="stock">
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
            <td class="px-20 py-4 whitespace-nowrap">
              <div class="text-sm text-gray-900">{{ stock.stockSymbol }}</div>
            </td>
            <td class="px-20 py-4 whitespace-nowrap">
              {{
                stock.askMin.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-20 py-4 whitespace-nowrap text-sm text-gray-900">
              {{
                stock.askMax.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-20 py-4 whitespace-nowrap text-sm text-gray-900">
              {{
                stock.bidMin.toLocaleString("pt-br", {
                  style: "currency",
                  currency: "BRL",
                })
              }}
            </td>
            <td class="px-20 py-4whitespace-nowrap text-sm text-gray-900">
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
      <div class="flex justify-between p-2">
        <button
          v-if="this.pg != 0"
          @click="getPrevios"
          class="inline-flex items-center py-2 px-4 mr-3 text-sm font-medium text-gray-500 bg-white rounded-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white"
        >
          <svg
            class="mr-2 w-5 h-5"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M7.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l2.293 2.293a1 1 0 010 1.414z"
              clip-rule="evenodd"
            ></path>
          </svg>
          Previous
        </button>

        <button
          v-if="this.pg < total_page - 1"
          @click="getNext"
          class="inline-flex items-center py-2 px-4 text-sm font-medium text-gray-500 bg-white rounded-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white justify-end"
        >
          Next
          <svg
            class="ml-2 w-5 h-5"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z"
              clip-rule="evenodd"
            ></path>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      stocks: [],
      seila1: [],
      seila: [],
      id_stock: "",
      dataSource: [],
      visualRange: [],
      page: [],
      pg: 0,
      total_page: "",
    };
  },
  created() {
    this.getPage();
  },
  methods: {
    async getPage() {
      this.claims = await this.$auth.getUser();
      let accessToken = this.$auth.getAccessToken();
      console.log(`Authorization: Bearer ${accessToken}`);
      console.log(this.pg + "Primeiro PG");
      try {
        let response = await axios.get(
          `http://localhost:8082/stocks/page?pageSize=10&pageNumber=${this.pg}&sort=id,asc`,
          {
            headers: { Authorization: "Bearer " + accessToken },
          }
        );
        console.log("estou aqui");
        this.page = response.data;
        this.total_page = this.page.totalPages;
      } catch (error) {
        this.page = `${error}`;
      }
    },

    getNext() {
      this.pg = this.pg + 1;
      console.log(this.pg + "Segundo PG");
      this.getPage();
    },
    getPrevios() {
      this.pg = this.pg - 1;
      this.getPage();
    },
  },
};
</script>
<style>
#chart-demo {
  height: 450px;
}

#zoomedChart {
  height: 315px;
  margin: 0 0 15px;
}

#chart-demo > div:not(#zoomedChart) {
  height: 120px;
}
</style>
