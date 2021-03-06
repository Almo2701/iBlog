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
      UserLogged: "",
      Userslst: [],
      ImgProfile: null,
      Description: "",
      DescriptionRules: [],
      Occupation: "",
      Occupation: [],
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
      // uploading image
      await storage
        .ref(this.UserName)
        .put(this.ImgProfile)
        .then((response) => {
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
      // getting image
      await storage
        .ref(this.UserName)
        .getDownloadURL()
        .then((response) => {
          this.ImageUrl = response;
          console.log(response);
        });

      if (this.ImageUrl !== null) {
        let userlog = {
          username: this.UserName,
          password: this.Password,
          UrlProfileImage: this.ImageUrl,
          occupation: this.Occupation,
          description: this.Description,
        };

        axios
          .post("https://localhost:44319/api/user", userlog)
          .then((response) => {
            if (response.data) {
              this.UserLogged = response.data;
              localStorage.UserLog = this.UserLogged;
            }
          });
      }
    },

    onchange(e) {
      this.ImgProfile = e.target.files[0];
    },
  },
};
</script>

        