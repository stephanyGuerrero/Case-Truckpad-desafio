<template>
  <v-app>
    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  data: () => ({
    //
  })
};
</script>
<style>
body{
  background-image: url("https://i0.wp.com/www.santafegrupo.com/wp-content/uploads/2017/08/Carretera-La-Paz-Centro-Malpaisillo-Grupo-Santa-Fe-HR.jpg?fit=1200%2C800&ssl=1");
  background-size: cover;
}

#app {
    background: transparent;
  }

</style>

