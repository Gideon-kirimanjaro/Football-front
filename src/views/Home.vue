<template>
  <v-card color="basil">
    <v-card-title class="text-center justify-center py-6">
      <h2 class="font-weight-bold  basil--text">
        Kirims Aggregator
      </h2>
    </v-card-title>

    <v-tabs v-model="tab" background-color="transparent" color="basil" grow>
      <v-tab v-for="item in items" :key="item">
        {{ item }}
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-card color="basil" flat>
          <v-card-text><About /></v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card color="basil" flat>
          <v-card-text
            ><h3><Fixtures /></h3
          ></v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card color="basil" flat>
          <v-card-text><Standings /></v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card color="basil" flat>
          <v-card-text><h3>4</h3></v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-card>
</template>

<script>
import About from "../components/About/About";
import Fixtures from "../components/Fixtures/Fixtures";
import Standings from "../components/Standings/Standings";
export default {
  name: "Home",
  components: {
    About,
    Fixtures,
    Standings,
  },
  data() {
    return {
      tab: null,
      items: ["About", "Fixtures", "Standings", "Stats"],
    };
  },
};
</script>
<style>
/* Helper classes */
.basil {
  background-color: #fffbe6 !important;
}
.basil--text {
  color: #356859 !important;
}
</style>
