<template lang="">
  <div class="account-pages my-5 pt-sm-5">
          <div class="container">
              <div class="row justify-content-center">
                  <div class="col-md-8 col-lg-6 col-xl-5">
                      <div class="text-center mb-4">
                          <a href="index.html" class="auth-logo mb-5 d-block">
                              <img src="assets/images/logo-dark.png" alt="" height="30" class="logo logo-dark">
                              <img src="assets/images/logo-light.png" alt="" height="30" class="logo logo-light">
                          </a>

                          <h4>Iniciar Sesión</h4>
                          <p class="text-muted mb-4">Sign in to continue to Chatvia.</p>

                      </div>

                      <div class="card">
                          <div class="card-body p-4">
                              <div class="p-3">
                                  <form action="index.html">
                                    <div class="mb-3">
                                        <label class="form-label">Correo</label>
                                        <div class="input-group mb-3 bg-soft-light rounded-3">
                                            <span class="input-group-text text-muted" id="basic-addon3">
                                                <i class="ri-user-2-line"></i>
                                            </span>
                                            <input type="email" v-model="user.email" required class="form-control form-control-lg border-light bg-soft-light" placeholder="Correo" aria-label="Enter Username" aria-describedby="basic-addon3">
                                        </div>
                                    </div>

                                    <div class="mb-4">
                                        <div class="float-end">
                                            <a href="auth-recoverpw.html" v-model="user.password" class="text-muted font-size-13">Olvidó la contraseña?</a>
                                        </div>
                                        <label class="form-label">Contraseña</label>
                                        <div class="input-group mb-3 bg-soft-light rounded-3">
                                            <span class="input-group-text text-muted" id="basic-addon4">
                                                <i class="ri-lock-2-line"></i>
                                            </span>
                                            <input type="password" required class="form-control form-control-lg border-light bg-soft-light" placeholder="Contraseña" aria-label="Enter Password" aria-describedby="basic-addon4">
                                        </div>
                                    </div>

                                      <div class="d-grid">
                                        <button class="btn btn-primary waves-effect waves-light" v-on:click="login()" type="submit">Iniciar Sesión</button>
                                      </div>

                                  </form>
                              </div>
                          </div>
                      </div>

                      <div class="mt-5 text-center">
                          <p>No tienes una cuenta ? <a href="/auth/register" class="fw-medium text-primary"> Registrarse </a> </p>
                          <p>© <script>document.write(new Date().getFullYear())</script> Chatvia. Crafted with <i class="mdi mdi-heart text-danger"></i> by Themesbrand</p>
                      </div>
                  </div>
              </div>
          </div>
      </div>
      <!-- end account-pages -->

</template>
<script>
export default {
  name: 'login',
  data() {
    return {
      url : process.env.API_BACKEND,
      user: {
        email: "",
        password: ""
      }
    }
  },
  methods: {
    login() {
      this.axios.post(`${API_URL}login`,this.user).then((response) => {
        this.$swal({
          title: 'Sesión iniciada',
          icon: 'success',
          confirmButtonText: 'OK',
          timer: 20000
        });
        localStorage.setItem("token",response.token);
        this.$router.push('home');
      }).
        catch((error)=>{
          this.$swal({
              title: 'Error',
              text: error.response.data,
              icon: 'error',
              confirmButtonText: 'OK',
              timer: 20000
          });
        });
    },
  }
}
</script>
<style lang="">

</style>
