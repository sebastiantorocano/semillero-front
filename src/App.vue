<template>
  <div>
    <div id="app" v-if="isAuth">
      <SPheader></SPheader>
      <SPleftMenu />
      <div class="content-wrapper">
        <router-view></router-view>
      </div>
      <SPfooter />
    </div>

    <div v-if="!isAuth && isVisitante == 'si'">
      <SPHeaderVisitante />

      <!--  <router-link
        to="/grupos_visitante"
        class="nav-item nav-link"
        style="text-align: center; font-size: 1.5em"
      >Ver grupos</router-link>-->
      <router-view></router-view>

      <SPfooter />
    </div>

    <div v-if="!isAuth && isVisitante == 'no'">
      <Login />
    </div>
  </div>
</template>

<script>
import SPheader from "./components/Header";
import SPleftMenu from "./components/LeftMenu";
import SPfooter from "./components/Footer";
import Login from "./views/Login";
import { TokenService } from "./services/storage.service";
import SPHeaderVisitante from "./components/HeaderVisitante";
import Principal from "./views/Principal";
// import SPVisitantes from "./views/VistaGruposVisitante";

export default {
  components: {
    SPheader,
    SPleftMenu,
    SPfooter,
    Login,
    SPHeaderVisitante,
    // SPVisitantes,
    Principal
  },
  data() {
    return {
      // auth: false
    };
  },
  created() {
    if (localStorage.access_token) {
      this.$store.commit("setLogin", true);
      // this.$store.commit('addUser', JSON.parse(localStorage.user))
    }

    this.$store.commit("setVisitante", "no");
    if (localStorage.visitante == "si") {
      this.$store.commit("setVisitante", "si");
    }

    if (localStorage.user) {
      var bytes = CryptoJS.AES.decrypt(localStorage.user, "Key");
      var originalText = bytes.toString(CryptoJS.enc.Utf8);
      /* console.log(originalText + "text"); */
      let user = JSON.parse(originalText);
      /* this.$store.state.user = user; */
      /* let user = JSON.parse(localStorage.user); */
      /* console.log(user) */
     
      let rol = user.id_rol;
      if (rol == 2) {
        this.$store.dispatch("infoUserDirector", user.id_usuario);
      } else if (rol == 3) {
        this.$store.dispatch("infoUserCoordinador", user.id_usuario);
      } else {
        this.$store.dispatch("infoUser", user.id_usuario);
      }
    }
  },
  computed: {
    isAuth() {
      return this.$store.state.isLogin;
    },
    isVisitante() {
      return this.$store.state.isVisitante;
    }
  }
};
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style>
</style>
