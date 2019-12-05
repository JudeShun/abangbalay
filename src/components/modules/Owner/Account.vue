
<template>
  <div class="text-center" id="account">
    <v-dialog v-model="dialog" width="350">
      <template v-slot:activator="{ on }">
        <v-card :loading="loading" class="mx-auto my-12" max-width="350" id="acc">
          <v-avatar color="indigo">
            <v-icon dark>mdi-account-circle</v-icon>
          </v-avatar>
          <v-card-title style="color:orange ; font-size: 25px">My Account</v-card-title>
          <v-card-text>
            <div>
              <v-text-field value="jeanilyntancinco@gmail.com" label="Email address" readonly></v-text-field>
              <v-text-field value="**********" label="Password" readonly></v-text-field>
            </div>
          </v-card-text>
          <v-card-actions>
            <v-btn color="deep-purple accent-4" text v-on="on">Edit</v-btn>
          </v-card-actions>
        </v-card>
      </template>

      <v-card>
        <v-card-title style="color:orange ; font-size: 25px">Edit account</v-card-title>
        <br>
        <v-card-text>

          <div>
            <v-text-field outlined prepend-inner-icon="mdi-email" dense label="Email address" v-model="email"></v-text-field>
            <v-text-field outlined prepend-inner-icon="mdi-lock" dense label="Password" v-model="password"></v-text-field>
            <v-text-field outlined prepend-inner-icon="mdi-lock" dense label="Confirm Password" v-model="cpassword"></v-text-field>
          </div>
        </v-card-text>

        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="deep-purple accent-4" text @click="dialog = true">Save</v-btn>
          <v-btn color="deep-purple accent-4" text @click="dialog = false">Cancel</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<style scoped>
#checkboxes {
  margin-top: -10% !important;
}

#acc {
  border: 1px gray !important;
}
</style>

<script>
import axios from "axios";
export default {
  data: () => ({
    dialog: false,
    loading: false,
    email: "",
    password: ""
  }),
  mounted() {
    axios
      .post("http://localhost:4000/user/register")
      .then(res => {
        this.email = res.data.email
        console.log(res.data)
      })
      .catch(err => {
        console.log(err);
      });
  },
  methods: {
    upload() {
      this.loading = true;
      setTimeout(() => (this.loading = false), 2000);
    },
    edit(e) {
      e.preventDefault();
      console.log("sds");
    }
  }
};
</script>