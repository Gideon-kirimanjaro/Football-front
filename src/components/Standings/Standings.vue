<template>
  <div>
    <v-col class="d-flex justify-center">
      <v-simple-table dark height="200">
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">
                Team
              </th>

              <th class="text-left">
                Matches
              </th>

              <th class="text-left">
                Won
              </th>
              <th class="text-left">
                Draw
              </th>
              <th class="text-left">
                Lost
              </th>
              <th class="text-left">
                Points
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in teams" :key="item.id">
              <td>{{ item.team }}</td>
              <td>{{ item.matchesPlayed }}</td>
              <td>{{ item.won }}</td>
              <td>{{ item.drawn }}</td>
              <td>{{ item.lost }}</td>
              <td>{{ item.points }}</td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </v-col>
  </div>
</template>

<script>
import db from "@/firebase";
export default {
  name: "Standings",
  data() {
    return {
      teams: [],
    };
  },
  methods: {
    getData() {
      db.ref("standings")
        .get()
        .then((snapshot) => {
          const data = snapshot.val();
          const values = Object.values(data);
          console.log("This is standings", values);
          const keys = Object.keys(data);
          const newTeams = [];
          values.forEach((val) => {
            newTeams.push({
              team: val.team,
              matchesPlayed: val.matchesPlayed,
              won: val.won,
              lost: val.lost,
              drawn: val.drawn,
              points: val.points,
            });
          });
          const newValues = newTeams
            .map((val) => {
              return val;
            })
            .sort((a, b) => {
              const a1 = a.points;
              const b1 = b.points;
              return b1 - a1;
            });
          this.teams = newValues;
          console.log("Here are your values", newValues);
        });
    },
  },
  created() {
    this.getData();
  },
  updated() {
    this.getData();
  },
};
</script>

<style lang="scss" scoped></style>
