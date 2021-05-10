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
              assists
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="player in scorers" :key="player.key">
            <td>{{ player.assistsPlayer }}</td>
            <td>{{ player.assistsTeam }}</td>
            <td>{{ player.assists }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </div>
</template>

<script>
import db from "@/firebase";
export default {
  name: "assists",
  data() {
    return {
      scorers: [],
    };
  },
  methods: {
    async getScorers() {
      try {
        db.ref("assists")
          .get()
          .then((snapshot) => {
            const data = snapshot.val();
            const values = Object.values(data);
            const scorers = [];
            const keys = Object.keys(values);
            values.forEach((val, index) => {
              scorers.push({
                key: index,
                assistsPlayer: val.assistName,
                assistsTeam: val.assistTeam,
                assists: val.assists,
              });
            });
            const newScorers = scorers
              .map((val) => {
                return val;
              })
              .sort((a, b) => {
                const assists1 = a.assistsNumber;
                const assists2 = b.assistsNumber;
                return assists2 - assists1;
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
