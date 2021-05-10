<template>
  <div>
    <v-simple-table dark>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">
              Name
            </th>
            <th class="text-left">
              Club
            </th>
            <th class="text-left">
              Goals
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in scorers" :key="player.key">
            <td>{{ player.scorerName }}</td>
            <td>{{ player.scorerClub }}</td>
            <td>{{ player.scorerGoals }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
import db from "@/firebase";
export default {
  name: "scorers",
  data() {
    return {
      scorers: [],
    };
  },
  methods: {
    async getScorers() {
      try {
        db.ref("scorers")
          .get()
          .then((snapshot) => {
            const data = snapshot.val();
            const values = Object.values(data);
            const scorers = [];
            const keys = Object.keys(values);
            values.forEach((val, index) => {
              scorers.push({
                key: index,
                scorerName: val.scorerName,
                scorerClub: val.scorerClub,
                scorerGoals: val.scorerGoals,
              });
            });
            const newScorers = scorers
              .map((val) => {
                return val;
              })
              .sort((a, b) => {
                const score1 = a.scorerGoals;
                const score2 = b.scorerGoals;
                return score2 - score1;
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
