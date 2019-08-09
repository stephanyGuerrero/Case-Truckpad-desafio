<template>
  <div>
    <v-layout align-center justify-center class="my-5">
      <v-flex md6 xs10>
        <v-img src="@/assets/logo-truckpad.png" alt />
      </v-flex>
    </v-layout>
    <v-layout wrap align-center justify-center class="my-5">
      <v-flex md12>
<v-layout wrap align-center justify-center class="my-5">
      <h2>Aqui pode Gerenciar seus Motoristas! </h2>
       </v-layout>
      </v-flex>
      
      <v-btn
        data-aos="zoom-in"
        data-aos-duration="2700"
        class="my-5"
        dark
        large
        href="/motorista"
      >comecar</v-btn>
      
    </v-layout>

    <v-layout align-center justify-center row fill-height>
      <v-flex class="my-5" md6>
        <v-card id="info" color="#385F73" dark>
          <v-card-text class="white--text">
            <div class="headline mb-2">Cadastre!</div>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>

    <v-layout align-center justify-end row fill-height>
      <v-flex class="my-5" md6>
        <v-card id="info" color="#385F73" dark>
          <v-card-text class="white--text">
            <div class="headline mb-2">Edite!</div>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>
<script>
import Aos from "aos";
export default {
  created() {
    Aos.init();
    console.log(Aos);
  }
};
</script>

<style scoped>
@import "./../../node_modules/aos/dist/aos.css";

#info {
  width: 380px;
}
</style>
