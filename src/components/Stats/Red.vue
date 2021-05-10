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
              Reds
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in scorers" :key="player.key">
            <td>{{ player.redPlayer }}</td>
            <td>{{ player.redTeam }}</td>
            <td>{{ player.redNumber }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
import db from "@/firebase";
export default {
  name: "Red",
  data() {
    return {
      scorers: [],
    };
  },
  methods: {
    async getScorers() {
      try {
        db.ref("redCards")
          .get()
          .then((snapshot) => {
            const data = snapshot.val();
            const values = Object.values(data);
            const scorers = [];
            const keys = Object.keys(values);
            values.forEach((val, index) => {
              scorers.push({
                key: index,
                redPlayer: val.redPlayer,
                redNumber: val.redNumber,
                redTeam: val.redTeam,
              });
            });
            const newScorers = scorers
              .map((val) => {
                return val;
              })
              .sort((a, b) => {
                const red1 = a.redNumber;
                const red2 = b.redNumber;
                return red2 - red1;
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
