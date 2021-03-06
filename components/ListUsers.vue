  
  <template>
  <section>
    <v-container class="text-center">
      <v-row class="mx-auto">
        <v-col>
          <template>
            <v-simple-table>
              <template v-slot:top>
                <v-toolbar flat>
                  <v-toolbar-title>Users Management</v-toolbar-title>
                  <v-divider class="mx-4" inset vertical></v-divider>
                  <v-spacer></v-spacer>
                  <v-dialog v-model="dialog" 
                  width="500px"
                  overflow="hidden">
                    <template v-slot:activator="{ on, attrs }">
                      <v-btn
                        color="primary"
                        dark
                        persistent
                        class="mt-auto"
                        v-bind="attrs"
                        v-on="on"
                      >
                        New Item
                      </v-btn>
                    </template>
                 <form-profile></form-profile>
                  </v-dialog>
                  <v-dialog v-model="dialogDelete" max-width="500px" >
                    <v-card>
                      <v-card-title class="headline"
                        >Are you sure you want to delete this
                        item?</v-card-title
                      >
                      <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn color="blue darken-1" text @click="close">
                          Cancel</v-btn
                        >
                        <v-btn color="blue darken-1" text>OK</v-btn>
                        <v-spacer></v-spacer>
                      </v-card-actions>
                    </v-card>
                  </v-dialog>
                </v-toolbar>
              </template>
              <template v-slot:default>
                <thead>
                  <tr>
                    <th class="text-left">Id</th>
                    <th class="text-left">Image</th>
                    <th class="text-left">Username</th>
                    <th class="text-left">Password</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="item in Userslst" :key="item.name">
                    <td>{{ item.userId }}</td>
                    <td>
                      <v-avatar class="elevation-8 my-5" size="70">
                        <v-img :src="item.urlProfileImage"></v-img>
                      </v-avatar>
                    </td>
                    <td>{{ item.username }}</td>
                    <td>{{ item.password }}</td>
                    <td>
                      <v-btn
                        :disabled="!valid"
                        color="primary"
                        class="ma-4 pa-4"
                        x-sm
                      >
                        Edit
                      </v-btn>
                    </td>
                    <td>
                      <v-btn
                        :disabled="!valid"
                        color="primary"
                        class="ma-4 pa-4"
                        @click="Delete(item.userId)"
                        x-sm
                      >
                        Delete
                      </v-btn>
                    </td>
                  </tr>
                </tbody>
              </template>
            </v-simple-table>
          </template>
        </v-col>
      </v-row>
    </v-container>
  </section>
</template>

<script>
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";
import axios from "axios";
import { storage } from "@/plugins/Firebase.js";
import FormProfile from "./FormProfile.vue";

export default {
  components: {
    Logo,
    VuetifyLogo,
    FormProfile,
  },

  data() {
    return {
      text: " txt",
      dialog: false,
      dialogDelete: false,
      valid: true,
      User: {
        username: "",
        mail: "",
        age: "",
        estatus: "",
        password: "",
      },
      UserLogged: "",
      Userslst: [],
    };
  },
  mounted() {
    this.getUsers();
  },
  methods: {
    validateForm() {
      this.$refs.form.validate();
    },
    close() {
      this.dialog = false;
    },
    getUsers() {
      axios.get("https://localhost:44319/api/user").then((response) => {
        this.Userslst = response.Users = response.data;
      });
    },

    Delete(id) {
      axios
        .delete("https://localhost:44319/api/user/" + id)
        .then((response) => {
          console.log("deleted");
          console.log(response);
          this.getUsers();
        });
    },
  },
};
</script>
        
  