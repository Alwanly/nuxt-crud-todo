<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" lg="6">
        <img
          src="https://treetan-storage.is3.cloudhost.id/assets/Image/illustrasi/login-image.png"
          loading="lazy"
          format="webp"
          sizes="sm:400px xxl:700px 2xl:800px"
        />
      </v-col>

      <v-col cols="12" lg="5" xl="4">
        <v-card-text>
          <v-row style="height: 60px">
            <v-col>
              {{ messageError }}
            </v-col>
            <v-col>
              {{ successMessage }}
            </v-col>
          </v-row>

          <v-row>
            <v-col cols="12">
              <h1 class="primary--text text-h3 text-lg-h2 font-fugaz">
                treetan
              </h1>
              <span> Raih Keberkahan Bersama</span>
            </v-col>
          </v-row>
          <v-form @submit.prevent="submit">
            <v-row>
              <v-col cols="12">
                <v-text-field v-model="email" label="Email" required />
              </v-col>

              <v-col cols="12">
                <v-text-field
                  v-model="password"
                  :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                  label="Password"
                  required
                  :counter="0"
                  :type="show1 ? 'text' : 'password'"
                  @click:append="show1 = !show1"
                />
              </v-col>
              <v-col cols="12">
                <v-row align="center">
                  <v-col cols="auto">
                    <v-checkbox
                      class="mt-0"
                      label="Remember Me "
                      color="primary"
                      value="red"
                      hide-details
                    />
                  </v-col>
                  <v-spacer />
                  <v-col>
                    <v-btn
                      text
                      plain
                      class="float-right pr-0"
                      to="forgot-password"
                    >
                      Lupa Password ?
                    </v-btn>
                  </v-col>
                </v-row>
              </v-col>
              <v-col cols="12" md="12">
                <v-btn
                  type="submit"
                  class="ma-2"
                  color="primary"
                  x-large
                  block
                  :loading="loading"
                >
                  Masuk
                </v-btn>
              </v-col>
              <v-col cols="12">
                <div class="d-flex flex-column align-center">
                  <h3 class="text--disabled font-weight-black">
                    Dasbor Travel
                  </h3>
                  <article class="text-center">
                    Treetan menawarkan kemudahan kepada rekanan travel untuk
                    mencapai target konsumen dengan mendigitalisasi proses
                    pemesanan umroh, halal tour dan domestic tour. Treetan
                    menyediakan sistem manajemen pelanggan dan inventaris yang
                    membantu rekanan travel dalam meningkatkan performa
                    penjualan.
                  </article>
                </div>
              </v-col>
            </v-row>
          </v-form>
        </v-card-text>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout: false,
  data() {
    return {
      email: '',
      password: '',
      show1: false,
      loading: false,
      successMessage: '',
      messageError: '',
    }
  },
  validations: {
    email: {
      required: true,
      email: true,
    },
    password: {
      required: true,
    },
  },
  methods: {
    oncloseAlert() {
      this.successMessage = ''
      this.messageError = ''
    },
    async submit() {
      this.loading = true
      await this.$axios
        .post('/api/auth/login', {
          email: this.email,
          password: this.password,
        })
        .then((response) => {
          this.loading = false
          this.$router.push('/app/dashboard')
        })
        .catch((error) => {
          this.loading = false
          this.messageError = error.response.data.message + 'tidak bisa nampil'
        })
    },
  },
}
</script>

<style></style>
