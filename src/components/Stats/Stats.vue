<template>
  <div>
    <v-card>
      <v-toolbar flat>
        <v-spacer></v-spacer>
        <template v-slot:extension>
          <v-tabs v-model="tabs" fixed-tabs>
            <v-tabs-slider></v-tabs-slider>
            <v-tab href="#mobile-tabs-5-1" class="primary--text">
              <h3>Scorers</h3>
              <v-icon>mdi-soccer</v-icon>
            </v-tab>

            <v-tab href="#mobile-tabs-5-2" class="red--text">
              <h3>Red Cards</h3>
              <v-icon>mdi-account-convert</v-icon>
            </v-tab>

            <v-tab href="#mobile-tabs-5-3" class="yellow--text">
              <h3>Yellow Cards</h3>
              <v-icon>mdi-account-convert-outline</v-icon>
            </v-tab>
            <v-tab href="#mobile-tabs-5-4" class="green--text bold">
              <h3>Assists</h3>
              <v-icon>mdi-account-reactivate</v-icon>
            </v-tab>
          </v-tabs>
        </template>
      </v-toolbar>

      <v-tabs-items v-model="tabs">
        <v-tab-item :value="'mobile-tabs-5-1'">
          <v-card flat>
            <Scorers />
          </v-card>
        </v-tab-item>
        <v-tab-item :value="'mobile-tabs-5-2'">
          <v-card flat>
            <Red />
          </v-card>
        </v-tab-item>
        <v-tab-item :value="'mobile-tabs-5-3'">
          <v-card flat>
            <Yellow />
          </v-card>
        </v-tab-item>
        <v-tab-item :value="'mobile-tabs-5-4'">
          <v-card flat>
            <Assists />
          </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card>
  </div>
</template>

<script>
import Scorers from "../Stats/Scorers";
import Red from "../Stats/Red";
import Yellow from "../Stats/Yellow";
import Assists from "../Stats/Assists";
export default {
  name: "Stats",
  components: {
    Scorers,
    Red,
    Yellow,
    Assists,
  },
  data() {
    return {
      tabs: null,
      data: [Scorers],
    };
  },
};
</script>

<style lang="scss" scoped></style>
