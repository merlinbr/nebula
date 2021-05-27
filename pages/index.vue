<template>
  <div class="container">
    <div>
      <h1 class="title">
        Nebula
      </h1>
      <div class="p-6 mt-5 max-w-sm mx-auto flex items-center space-x-4">
        <template v-if="showLogin">
          <Login @toggle-login="toggleLogin"/>
        </template>
        <template v-else>
          <SignUp @toggle-login="toggleLogin"/>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showLogin: true,
      userData: null,
    }
  },

  mounted() {
    // this.getAccount()
  },

  methods: {
    toggleLogin(login) {
      if (login) {
        this.showLogin = true
      } else {
        this.showLogin = false
      }
    },
    getAccount() {
      // TODO: check store for existing token
      this.$axios.get('https://api.spacetraders.io/my/account', {
        headers: {
          Authorization: 'Bearer ' + this.token
        }
      }).then(response => {
        this.user = response.data.user
      }).catch(error => {
        console.error(error)
      })
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Zen Dots', cursive;
  display: block;
  font-weight: 300;
  font-size: 50px;
  color: #00b6ca;
  letter-spacing: 1px;
}
</style>
