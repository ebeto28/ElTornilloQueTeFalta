                <template>
  <div class="container">
    <div class="columns">
      <div class="column is-6 is-offset-3">
        <h3 class="title is-3">Crear Cuenta</h3>
        <hr />
        <form action="#" @submit.prevent="register">
          <div class="field">
            <label class="label">Nombre</label>
            <div class="control">
              <input class="input" type="text" placeholder="Nombre" v-model="name" />
              {{name}}
            </div>
          </div>

          <div class="field">
            <label class="label">Email</label>
            <div class="control">
              <input class="input" type="email" v-model="email" />
              {{email}}
            </div>
          </div>

          <div class="field">
            <label class="label">Contraseña</label>
            <div class="control">
              <input class="input" type="password" v-model="password" />
              {{password}}
            </div>
          </div>

          <button type="submit" class="button is-primary">Registrarme</button>
        </form>
        <br />

        <div class="notification is-danger" v-if="error">{{error}}</div>
      </div>
    </div>
  </div>
</template>

    <script>
import db from "@/firebase/init";
import firebase from "firebase";
import { mapMutations, mapGetters } from "vuex";
import { mapState } from "vuex";

export default {
  data() {
    return {
      name: "",
      email: "",
      password: "",
      error: ""
    };
  },
  name: "Register",
  methods: {
    register() {
      this.error = "";
      if (this.name && this.email && this.password) {
        firebase
          .auth()
          .createUserWithEmailAndPassword(this.email, this.password)
          .then(user => {
            this.$router.push({ name: "getCliente" });
            console.log(user);
            this.registrarEmail(this.email);
            console.log(db);
          })
          .catch(err => {
            this.error = err.message;
          });

        //enviamos
      } else {
        this.error = "Todos los campos son requeridos";
      }
    },
     ...mapMutations(["registrarEmail", "limpiarEmail"])
    
  },
  computed: {
    ...mapState(["idemail"]),
    ...mapGetters(["getemail"]),
    ...mapState(["id"]),
    ...mapGetters(["getid"])
  }
};
</script>