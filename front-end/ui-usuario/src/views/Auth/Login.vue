                <template>
  <div class="container">
    <div class="columns">
      <div class="column is-6 is-offset-3">
        <h3 class="title is-3">Iniciar Sesion</h3>
        <hr />
        <form action="#" @submit.prevent="login">
          <!--     <div class="field">
                        <label class="label">Nombre</label>
                        <div class="control">
                            <input class="input" type="text" placeholder="Nombre" v-model="name" />
                            {{name}}
                        </div>
          </div>-->

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

          <button type="submit" class="button is-primary">Iniciar Sesion</button>
        </form>
        <br />

        <div class="notification is-danger" v-if="error">{{error}}</div>
      </div>
    </div>
  </div>
</template>



    <script>

   

import {mapMutations, mapGetters} from 'vuex';
import {mapState} from 'vuex';

import db from '@/firebase/init'; 
import firebase from 'firebase';

export default {
  data() {
    return {
     
      email: "",
      password: "",
      error: "",
      BDmail:"",
      BDid:"",
    };
  },
  name: "Login",
  methods: {
    login() {
        this.error='';

      if ( this.email && this.password) {
          firebase.auth().signInWithEmailAndPassword(this.email, this.password)
          .then(user => {
              this.$router.push({name: 'getCliente'})

               console.log(user);
                console.log(db); 

                this.registrarEmail(this.email);

                console.log( "una pa;abra",this.$store.state.idemail);
                console.log("*****************************");



          }).catch(err=>{
              this.error= err.message

          })
        //enviamos
      } else {
        this.error = "Todos los campos son requeridos";
      }
    },
    limpiarEmail(){
      this.limpiarEmail();
      
    },
    ...mapMutations(['registrarEmail','limpiarEmail'])

  },
  computed: {
        ...mapState(['idemail']),
        ...mapGetters(['getemail'])

    }

};
</script>