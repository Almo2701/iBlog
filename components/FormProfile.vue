
<style>
@import url("https://fonts.googleapis.com/css2?family=Merienda&display=swap");
</style>
<template>
  <section>
    <v-card>
      <v-row>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation class="mx-12">
            <h5 class="my-7 display-1">New Post</h5>
            <v-text-field
              solo
              v-model="Title"
              :rules="TitleRules"
              label="Title"
              class=""
              required
            ></v-text-field>
            <v-textarea
              solo
              v-model="Description"
              :rules="DescriptionRules"
              label="Description"
              required
            ></v-textarea>

            <input
              type="file"
              ref="img"
              @change="onchange"
              label="Image Profile"
            />

            <v-row>
              <v-col md="12" align="center">
                <v-btn
                  :disabled="!valid"
                  color="primary"
                  class="my-5"
                  @click="Post()"
                  medium
                >
                  Publish
                </v-btn>
              </v-col>
            </v-row>
          </v-form>
        </v-card-text>
      </v-row>
    </v-card>
  </section>
</template>


<script>
import Logo from "~/components/Logo.vue";
import VuetifyLogo from "~/components/VuetifyLogo.vue";
import axios from "axios";
import { auth } from "@/plugins/Firebase.js";
import { storage } from "@/plugins/Firebase.js";

export default {
  components: {
    Logo,
    VuetifyLogo,
  },

  data() {
    return {
      text: " txt",
      valid: true,
      ImgPost: null,
      ImgPostLst:[],
      Title: "",
      TitleRules: [
        // (x) => (x && x.length >= 5) || "Name must have 10 characters",
        // (x) => /.+@.+/.test(x) || "E-mail must be valid",
      ],
      Description: "",
      DescriptionRules: [
        // (m) => (m && m.length >= 6) || "PassWord must have 6 characters",
      ],
    };
  },
  methods: {
    validateForm() {
      this.$refs.form.validate();
    },

    async Post() {
    
      let User=JSON.parse(localStorage.UserLog);
      // uploading image
      await storage
        .ref('PostImage/'+User.username+'/'+this.Title)
        .put(this.ImgPost)
        .then((response) => {
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
      // getting image
      await storage
        .ref('PostImage/'+User.username+'/'+this.Title)
        .getDownloadURL()
        .then((response) => {
          this.ImgPost = response;
          console.log(response);
        });

      if (this.ImageUrl !== null) {
        let Post = {
          title: this.Title,
          description: this.Description,
          urlImage: this.ImgPost,
          userId: User.userId,
          date: "2021-02-02",
        };
   console.log(Post)
        axios
          .post("https://localhost:44319/api/post", Post)
          .then((response) => {
            console.log(response)
            location.href='/'
            
          }).catch(error=>{
              console.log(error)
          });

     
      }
    },

    onchange(e) {
      this.ImgPost = e.target.files[0];
    },
  },
};
</script>

        