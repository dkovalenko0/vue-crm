<template>
  <div>
    <div class="page-title">
      <h3>Счет</h3>

      <button class="btn waves-effect waves-light btn-small" @click="refresh">
        <i class="material-icons">refresh</i>
      </button>
    </div>

    <Loader v-if="loading"></Loader>

    <div class="row" v-else>
      <HomeBill :rates="currency.rates"></HomeBill>
      <HomeCurrency
        :rates="currency.rates"
        :date="currency.date"
      ></HomeCurrency>
    </div>
  </div>
</template>

<script>
import HomeBill from "@/components/HomeBill";
import HomeCurrency from "@/components/HomeCurrency";

export default {
  name: "Home",
  metaInfo() {
    return {
      title: this.$title("Menu_Bill")
    };
  },
  data: () => ({
    loading: true,
    currency: null
  }),
  async mounted() {
    this.currency = await this.$store.dispatch("fetchCurrency");
    this.loading = false;
  },
  methods: {
    async refresh() {
      this.loading = true;
      this.currency = await this.$store.dispatch("fetchCurrency");
      this.loading = false;
    }
  },
  components: {
    HomeBill,
    HomeCurrency
  }
};
</script>
