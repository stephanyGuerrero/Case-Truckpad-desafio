<template>
  <div>
    <v-flex class="ma-5" id="init-css">
      <v-layout align-center justify-center class="my-5">
        <v-flex md6 xs10>
          <v-img src="@/assets/logo-truckpad.png" alt />
        </v-flex>
      </v-layout>

      <v-layout wrap align-center justify-center class="my-5">
        <v-flex xs12 md12>
          <v-layout wrap align-center justify-center class="my-5 mx-2">
            <h2>Aqui você pode Gerenciar seus Motoristas!</h2>
          </v-layout>
        </v-flex>

        <v-btn
          id="start"
          data-aos="zoom-in"
          data-aos-duration="3000"
          class="my-5 elevation-5"
          dark
          large
          href="/motorista"
        >começar</v-btn>
      </v-layout>

      <v-layout align-center justify-center row fill-height>
        <v-flex class="my-5 mx-5" md6 xs11>
          <v-layout align-center justify-start row fill-height>
            <div class="elevation-5" data-aos="zoom-out" data-aos-duration="1000" id="info" dark>
              <div id="text" class="mx-5 my-2">Você consegue Cadastrar!</div>
            </div>
          </v-layout>
        </v-flex>
      </v-layout>

      <v-layout align-center justify-center row fill-height>
        <v-flex class="my-5 mx-5" md6 xs11>
          <v-layout align-center justify-end row fill-height>
            <div class="elevation-5" data-aos="zoom-out" data-aos-duration="1800" id="info" dark>
              <div id="text" class="mx-5 my-2">Você pode Editar seus cadastros!</div>
            </div>
          </v-layout>
        </v-flex>
      </v-layout>

      <v-layout wrap align-center justify-center class="my-5">
        <v-flex class="mb-5" xs11 md12>
          <v-layout wrap align-center justify-center>
            <div id="note">
              <h4
                class="ma-5"
              >Isto é um aplicativo teste, ou seja, apenas uma simulação de um gerenciador de motoristas :)</h4>
            </div>
          </v-layout>
        </v-flex>
      </v-layout>
    </v-flex>
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
  height: 49px;
  width: 380px;
  border-radius: 13px;
  text-shadow: 2px 2px black;
  color: white;
  background-color: rgba(56, 95, 115, 0.712);
}

#text {
  font-size: 20px;
}

#start {
  border-radius: 20px;
  width: 160px;
  height: 70px;
  font-size: 20px;
}

#init-css {
  background-color: rgba(255, 255, 0, 0.267);
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}
h4 {
  color: azure;
  text-shadow: 1px 1px black;
}

h2 {
  text-shadow: 2px 2px rgba(214, 214, 214, 0.767);
}

#note {
  border-radius: 18px;
  border-color: rgb(112, 99, 99);
  background-color: rgba(75, 107, 148, 0.493);
}
</style>
