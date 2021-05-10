<template>
  <v-app>
    <v-main>
      <router-view />
      <div class="copy">
        <v-footer padless>
          <v-col class="text-center" cols="12">
            {{ new Date().getFullYear() }} — <strong>@GideonKirimanjaro</strong>
          </v-col>
        </v-footer>
      </div>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
<style>
* {
  font-family: "Montserrat";
  src: url("./assets/fonts/Montserrat-Regular.ttf");
}
.copy {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  color: white;
  text-align: center;
}
</style>
