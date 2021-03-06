
<template>
  <v-container>
    <section>
      <v-row align="center" class="mt-15" id="Login">
        <v-col align="center">
          <v-card style="max-width: 400px" class="elevation-14">
            <v-row>
              <v-col cols="12">
                <v-avatar class="elevation-8 my-3" size="105" align="center">
                  <v-img
                    src="https://image.freepik.com/vector-gratis/hombre-muestra-gesto-gran-idea_10045-637.jpg"
                  ></v-img>
                </v-avatar>
              </v-col>
            </v-row>
            <v-row>
              <v-card-text class="ma-auto">
                <v-form
                  ref="form"
                  v-model="valid"
                  lazy-validation
                  class="mx-12"
                >
                  <v-text-field
                    v-model="UserName"
                    :rules="UserNameRules"
                    label="Name"
                    class="pa-4"
                    required
                  ></v-text-field>
                  <v-text-field
                    v-model="Password"
                    type="password"
                    :counter="20"
                    :rules="PasswordRules"
                    label="Password"
                    class="pa-4"
                    required
                  ></v-text-field>

                  <v-row>
                    <v-col md="12">
                      <v-btn
                        :disabled="!valid"
                        color="primary"
                        class="ma-4 pa-4"
                        @click="logIn"
                        x-large
                      >
                        Log in
                      </v-btn>
                    </v-col>
                  </v-row>
                </v-form>
              </v-card-text>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </section>
  </v-container>
</template>


<script>
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";
import FormProfile from "../components/FormProfile.vue";
import axios from "axios";
import swal from "sweetalert";

export default {
  components: {
    Logo,
    VuetifyLogo,
    FormProfile,
  },

  data() {
    return {
      text: " txt",
      valid: true,
      UserLogged: "",
      Userslst: [],
      ImgProfile: null,
      UserName: "",
      UserNameRules: [
        // (x) => (x && x.length >= 5) || "Name must have 10 characters",
        // (x) => /.+@.+/.test(x) || "E-mail must be valid",
      ],
      Password: "",
      PasswordRules: [
        // (m) => (m && m.length >= 6) || "PassWord must have 6 characters",
      ],
    };
  },
  methods: {
    validateForm() {
      this.$refs.form.validate();
    },

    async logIn() {
      localStorage.UserLog = "";

      const userlog = {
        username: this.UserName,
        password: this.Password,
      };
      console.log(userlog);
      axios
        .post("https://localhost:44319/api/login", userlog)
        .then((response) => {
          if (response) {
            this.UserLogged = response.data;
            localStorage.UserLog = JSON.stringify(response.data);
            swal({
              title: "Log Succesfully!",
              icon: "success",
              onClose:this.onClose()
            })

          }
        });

       
    },
     onClose(){

        location.href="/"
     },

    onchange(e) {
      this.ImgProfile = e.target.files[0];
    },
  },
};
</script>

        