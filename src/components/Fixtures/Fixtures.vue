<template>
  <div>
    <v-col class="d-flex justify-center">
      <v-simple-table dark>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">
                Away
              </th>
              <th class="text-left"></th>
              <th class="text-left">
                Home
              </th>

              <th class="text-left">
                Date
              </th>
              <th class="text-left">
                time
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in teams" :key="item.id">
              <td>{{ item.away }} {{ item.awayScore }}</td>
              <td>vs</td>
              <td>{{ item.home }} {{ item.homeScore }}</td>
              <td>{{ item.date }}</td>
              <td>{{ item.time }}</td>
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
  name: "Fixtures",
  data() {
    return {
      teams: [],
    };
  },
  methods: {
    getData() {
      db.ref("fixtures")
        .get()
        .then((snapshot) => {
          const data = snapshot.val();
          const values = Object.values(data);
          const keys = Object.keys(data);
          const newTeams = [];
          values.forEach((val) => {
            newTeams.push({
              away: val.away,
              awayScore: val.awayScore,
              home: val.home,
              homeScore: val.homeScore,
              date: val.date,
              time: val.time,
            });
          });
          const newValues = newTeams
            .map((val) => {
              return val;
            })
            .sort((a, b) => {
              const a1 = a.date;
              const b1 = b.date;
              return new Date(b1) - new Date(a1);
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
