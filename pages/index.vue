<script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
<template >
  <div id="app">
    <v-app-bar
      absolute
      color="white"
      elevate-on-scroll
      scroll-target="#scrolling-techniques-7"
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>My Blog</v-toolbar-title>

      <v-spacer></v-spacer>
    </v-app-bar>

    <!-- <section id="Main">
      <v-row no-gutters>
        <v-img
          :min-height="'calc(100vh - ' + $vuetify.application.top + 'px)'"
          src="https://images.unsplash.com/photo-1604329051903-d89ddd523330?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=751&q=80"
        >
          <v-theme-provider dark>
            <v-container fill-height>
              <v-row align="center" class="white--text" justify="center">
                <v-col class="white--text text-center" cols="12" tag="h1">
                  <span class="font-weight-light"> WELCOME TO </span>

                  <br />

                  <span
                    :class="[
                      $vuetify.breakpoint.smAndDown ? 'display-3' : 'display-4',
                    ]"
                    class="font-weight-black"
                  >
                    Vuetify
                  </span>
                </v-col>

                <v-btn
                  class="align-self-end"
                  fab
                  outlined
                  @click="$vuetify.goTo('#Userslst')"
                >
                  <v-icon>mdi-chevron-double-down</v-icon>
                </v-btn>
              </v-row>
            </v-container>
          </v-theme-provider>
        </v-img>
      </v-row>
    </section> -->
    <v-container>
      <section id="about-me" class="my-5">
        <div class="py-4"></div>

        <v-container class="text-center">
          <h2 class="display-1 mb-3">{{ User.username }}</h2>

          <v-responsive class="mx-auto mb-8" width="116">
            <v-divider class="mb-1 mt-2"></v-divider>
          </v-responsive>
          <v-avatar class="elevation-12 mb-12" size="200">
            <v-img
            :src ="User.urlProfileImage"></v-img>
          </v-avatar>

          <div></div>
          <span class="grey--text text--darken-1 font-weight-bold">
            {{ User.occupation }}
          </span>

          <div class="mt-5">
            <v-btn class="" text icon color="red lighten-2">
              <v-img
                src="https://www.flaticon.es/svg/vstatic/svg/725/725289.svg?token=exp=1614957895~hmac=bd3ab3f0256a1d474a2e16610ba2b518"
                max-width="20"
              >
              </v-img>
            </v-btn>

            <v-btn class="" text icon color="red lighten-2">
              <v-img
                src="https://www.flaticon.es/svg/vstatic/svg/725/725311.svg?token=exp=1614957895~hmac=e391f3ef042a5acfeb03ac5615354100"
                max-width="20"
              >
              </v-img>
            </v-btn>
            <v-btn class="" text icon color="red lighten-2">
              <v-img
                src="https://www.flaticon.es/svg/vstatic/svg/725/725298.svg?token=exp=1614957895~hmac=675ef7bef37f16900652c2c7567c817b"
                max-width="20"
              >
              </v-img>
            </v-btn>
            <v-btn class="" text icon color="red lighten-2">
              <v-img
                src="https://www.flaticon.es/svg/vstatic/svg/725/725320.svg?token=exp=1614957895~hmac=a6b892e0b2c64b10d1255c738ba18b32"
                max-width="20"
              >
              </v-img>
            </v-btn>
          </div>

          <v-responsive class="mx-auto my-8 mb-8 body-1" max-width="720">
            {{ User.description }}
          </v-responsive>

          <div class="mt-12 mx-8">
            <v-row>
              <v-col
                v-for="item in Postlist"
                :key="item.postId"
                 cols="4"
              >
                <!-- <v-hover v-slot="{ hover }">
                  <div
                    v-if="hover"
                    style="height: 100%"
                    class="d-flex imageHover transition-fast-in-fast-out blue darken-2"
                  >
                    <h5>title</h5>
                  </div>

                  
                </v-hover> -->
                <v-img
                  :src="item.urlImage"
                  aspect-ratio="1"
                  class="grey lighten-2 elevation-8"
                >
                  <template v-slot:placeholder>
                    <v-row
                      class="fill-height ma-0"
                      align="center"
                      justify="center"
                    >
                      <v-progress-circular
                        indeterminate
                        color="grey lighten-5"
                      ></v-progress-circular>
                    </v-row>
                  </template>
                </v-img>
              </v-col>
            </v-row>
          </div>
        </v-container>

        <div class="py-12"></div>
      </section>
      <v-dialog v-model="dialog" width="500px">
        <template v-slot:activator="{ on, attrs }">
          <v-card-text style="height: 100px; position: relative">
            <v-fab-transition>
              <v-btn
                color="orange"
                class="elevation-12 mx-5"
                dark
                fixed
                bottom
                right
                fab
                v-bind="attrs"
                v-on="on"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </v-fab-transition>
          </v-card-text>
        </template>
        <form-profile></form-profile>
      </v-dialog>

      <!-- <v-row>
       <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Username
          </th>
          <th class="text-left">
            Password
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in Users"
          :key="item.username"
        >
          <td>{{ item.username }}</td>
          <td>{{ item.password }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
    </v-row> -->
    </v-container>
    <list-users id="Userslst"></list-users>
    <v-footer class="py-8"></v-footer>
  </div>
</template>
<style scoped>
.Imagehover {
  align-items: center;
  bottom: 0;
  justify-content: center;
  opacity: 0.5;
  position: absolute;
  width: 100%;
}
</style>
<script>
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";
import Login from "~/components/Login.vue";
import axios from "axios";
import { storage } from "@/plugins/Firebase.js";
import ListUsers from "../components/ListUsers.vue";

export default {
  components: {
    Logo,
    VuetifyLogo,
    Login,
    ListUsers,
  },

  data() {
    return {
      valid: true,
      User: JSON.parse(localStorage.UserLog),

      UserLogged: "",
      Userslst: [],
      absolute: true,
      overlay: false,
      UserName: "",
      Postlist: [],
      ImgPostLst: [],
      UserNameRules: [
        (x) => (x && x.length <= 100) || "Name must have 10 characters",
      ],
      Password: "",
      PasswordRules: [
        (m) => (m && m.length <= 65) || "PassWord must have 5 characters",
      ],
      dialog: false,
      Message: "",
    };
  },

  mounted() {
    axios.get("https://localhost:44319/api/post").then((response) => {
      this.Postlist = response.Users = response.data;
      console.log(this.Postlist);
      console.log("data");

        storage
        .ref('ProfileImage/Alam Mena Beato.jpg')
        .getDownloadURL()
        .then((response) => {
          console.log(response);
        });
    });
  },

  methods: {
    validateForm() {
      this.$refs.form.validate();
    },
  },
};
</script>
