<template>
  <section class="hero is-success is-fullheight">
    <div class="hero-body">
      <div class="container has-text-centered">
        <div class="column is-4 is-offset-4">
          <h3 class="title has-text-grey">Login</h3>
          <p class="subtitle has-text-grey">Please login to proceed.</p>
          <div class="box">
            <figure class="avatar">
              <img src="https://via.placeholder.com/300">
            </figure>
            <form>
              <div class="field">
                <div class="control">
                  <input class="input is-large"
                         v-model="form.email"
                         @blur="$v.form.email.$touch()"
                         type="email"
                         placeholder="Your Email"
                         autofocus=""
                         autocomplete="email">
                  <div v-if="$v.form.email.$error" class="form-error">
                    <span class="help is-danger" v-if="!$v.form.email.required">Email is required</span>
                    <span class="help is-danger" v-if="!$v.form.email.emailValidator">Email address is not valid</span>
                  </div>
                </div>
              </div>
              <div class="field">
                <div class="control">
                  <input
                      class="input is-large"
                      v-model="form.password"
                      @blur="$v.form.password.$touch()"
                      type="password"
                      placeholder="Your Password"
                      autocomplete="current-password">
                  <div class="form-error" v-if="$v.form.password.$error">
                    <span class="help is-danger" v-if="!$v.form.password.required">Password is required</span>
                  </div>
                </div>
              </div>
              <!-- Login Button -->
              <button
                  @click.prevent="login"
                  :disabled="$v.form.$invalid"
                  class="button is-block is-info is-large is-fullwidth">
                Login
              </button>
            </form>
          </div>
          <p class="has-text-grey">
            <a>Sign In With Google</a> &nbsp;??&nbsp;
            <nuxt-link to="/register">Sign Up</nuxt-link> &nbsp;??&nbsp;

            <a href="../">Need Help?</a>
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import {required, email} from 'vuelidate/lib/validators'
export default {
  data(){
    return{
      form: {
        email: '',
        password: ''
      },
    }
  },
  validations:{
    form: {
      email: {
        emailValidator: email,
        required
      },
      password: {
        required
      }
    },
  },
  computed:{
    isFormValid(){
      return !this.$v.$invalid
    }
  },
  methods:{
    login(){
      this.$v.form.$touch()

      if (this.isFormValid){
        this.$store.dispatch('auth/login', this.form)
            .then(() => {
              this.$router.push('/')
            })
      }
    }
  }
}
</script>

<style scoped>
.hero.is-success {
  background: #F2F6FA;
}
.hero .nav, .hero.is-success .nav {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.box {
  margin-top: 5rem;
}
.avatar {
  margin-top: -70px;
  padding-bottom: 20px;
}
.avatar img {
  height: 128px;
  width: 128px;
  padding: 5px;
  background: #fff;
  border-radius: 50%;
  -webkit-box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
  box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
}
p.subtitle {
  padding-top: 1rem;
}
</style>
