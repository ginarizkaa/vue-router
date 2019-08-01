<template>
  <q-page>
    <div class="flex flex-center">
      <div class="q-pa-md" style="max-width: 350px; width:100%">
        <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
          <q-input
            filled
            v-model="email"
            label="Your email *"
            hint="Employee Email"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          />

          <q-input
            filled
            v-model="password"
            label="Your password *"
            hint="Employee Password"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Please type something']"
          />

          <div>
            <!-- <q-btn to="/register" label="To Docs index" outline color="purple" /> -->
            <q-btn label="Login" type="submit" color="primary"/>
            <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
          </div>
        </q-form>
      </div>
    </div>
  </q-page>
</template>

<script>
import employee from "../api/employee/index";
import { constants } from 'crypto';

export default {
  data() {
    return {
      email: "",
      password: "",
      employeeData: []
    };
  },

  methods: {
    onSubmit() {
      let self = this;

      //console.log(self.$router)

      employee
      .getLogin(window, self.email, self.password)
      .then(function(result){
          if(!result){
             self.$q.notify({
              color: "red-5",
              textColor: "white",
              icon: "fas fa-exclamation-triangle",
              message: "You need to accept the license and terms first"
            });
          }else {
            self.$q.notify({
              color: "green-4",
              textColor: "white",
              icon: "fas fa-check-circle",
              message: "Anda Telah Login"
            })
            self.$router.push('register')
          }
          return result;
      })
      .catch(function(err){
          console.log(err);
      })
    },

    onReset() {
      this.name = null;
      this.age = null;
      this.accept = false;
    }
  }
};
</script>

