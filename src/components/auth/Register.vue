<template>
   <div>
      <div class="my-5 text-center col-8 offset-2">
         <img src="@/assets/welcome.svg" class="img-fluid" />
      </div>

      <div class="text-center">
         <h2>Jetzt Registrieren</h2>
         <p>
            oder
            <a class="text-vue2" role="button" @click="changeComponent('Login')"
               >melden Sie sich mit Ihrem Konto an</a
            >
         </p>
      </div>

      <div class="alert alert-danger col-8 offset-2" v-if="error !== ''">
         {{ displayErrorText }}
      </div>

      <Form
         @submit="submitData"
         :validation-schema="schema"
         v-slot="{ errors }"
      >
         <div class="form-row">
            <div class="form-group col-md-8 offset-2">
               <label for="email"><strong>E-Mail-Adresse</strong></label>
               <Field
                  as="input"
                  name="email"
                  type="email"
                  class="form-control"
                  id="email"
               />
               <small class="text-danger" v-if="errors.email">
                  {{ errors.email }}
               </small>
            </div>
         </div>
         <div class="form-row">
            <div class="form-group col-md-8 offset-2">
               <label for="password"><strong>Passwort</strong></label>
               <Field
                  as="input"
                  name="password"
                  type="password"
                  class="form-control"
                  id="password"
               />
               <small class="text-danger" v-if="errors.password">
                  {{ errors.password }}
               </small>
            </div>
         </div>
         <div class="form-row">
            <div class="form-group col-md-8 offset-2">
               <label for="confirmPassword"
                  ><strong>Passwort wiederholen</strong></label
               >
               <Field
                  as="input"
                  name="confirmPassword"
                  type="password"
                  class="form-control"
                  id="confirmPassword"
               />
               <small class="text-danger" v-if="errors.confirmPassword">
                  {{ errors.confirmPassword }}
               </small>
            </div>
         </div>
         <div class="form-row mt-3">
            <div class="form-group col-md-8 offset-2">
               <button class="btn bg-vue">
                  <span v-if="!isLoading">Registrieren</span>
                  <span v-else class="spinner-border spinner-border-sm"></span>
               </button>
            </div>
         </div>
      </Form>
   </div>
</template>


<script>
import { Form, Field } from "vee-validate";
import * as yup from "yup";

export default {
   name: "TheRegister",

   components: {
      Form,
      Field,
   },

   emits: {
      "change-component": (payload) => {
         if (payload.componentName !== "Login") {
            return "";
         } else {
            return "Login";
         }
      },
   },

   data() {
      const schema = yup.object().shape({
         email: yup
            .string()
            .required("Email-Adresse wird ben??tigt.")
            .trim()
            .email("Das ist keine g??ltige E-Mail"),
         password: yup
            .string()
            .required("Ein Passwort wird ben??tigt.")
            .min(6, "Das Passwort muss mindestens 6 Zeichen lang sein."),
         confirmPassword: yup
            .string()
            .oneOf([yup.ref("password")], "Passw??rter stimmen nicht ??berein."),
      });

      return {
         schema,
         error: "",
         isLoading: false,
      };
   },

   computed: {
      displayErrorText() {
         if (this.error !== "") {
            if (this.error.includes("EMAIL_EXISTS")) {
               return "Die E-Mail Adresse existiert bereits.";
            } else {
               return "Es ist ein unbekannter Fehler aufgetreten. Bitte versuchen Sie es noch einmal";
            }
         } else {
            return "";
         }
      },
   },

   methods: {
      submitData(values) {
         this.isLoading = true;
         this.error = "";
         // console.log(values);
         this.$store
            .dispatch("signup", {
               email: values.email,
               password: values.password,
            })
            .then(() => {
               this.isLoading = false;
               this.changeComponent("Login");
               // console.log(this.$store.state);
            })
            .catch((error) => {
               this.error = error.message;
               this.isLoading = false;
            });
      },

      changeComponent(componentName) {
         this.$emit("change-component", { componentName });
      },
   },
};
</script>


<style scoped>
.btn {
   width: 100%;
}
</style>