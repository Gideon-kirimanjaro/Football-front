<template>
  <div>
    <v-simple-table dark>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              Player
            </th>
            <th class="text-left">
              Team
            </th>
            <th class="text-left">
              yellows
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in scorers" :key="player.key">
            <td>{{ player.yellowPlayer }}</td>
            <td>{{ player.yellowTeam }}</td>
            <td>{{ player.yellowNumber }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
import db from "@/firebase";
export default {
  name: "Yellow",
  data() {
    return {
      scorers: [],
    };
  },
  methods: {
    async getScorers() {
      try {
        db.ref("yellowCards")
          .get()
          .then((snapshot) => {
            const data = snapshot.val();
            const values = Object.values(data);
            const scorers = [];
            const keys = Object.keys(values);
            values.forEach((val, index) => {
              scorers.push({
                key: index,
                yellowPlayer: val.yellowName,
                yellowNumber: val.yellowNumber,
                yellowTeam: val.yellowClub,
              });
            });
            const newScorers = scorers
              .map((val) => {
                return val;
              })
              .sort((a, b) => {
                const yellow1 = a.yellowNumber;
                const yellow2 = b.yellowNumber;
                return yellow2 - yellow1;
              });
            this.scorers = newScorers;
          });
      } catch {
        console.log("There is an error getting your data");
      }
    },
  },
  created() {
    this.getScorers();
  },
  updated() {
    this.getScorers();
  },
};
</script>

<style lang="scss" scoped></style>
