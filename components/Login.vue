<template>
  <div class="grid grid-cols-1">
    <label class="block mb-5">
      <span class="text-white float-left">Token</span>
      <input
        v-model="token"
        type="text"
        ref="token"
        class="mt-0 w-full block px-0.5 border-b text-white border-turquoise-500 focus:outline-none focus:border-b-4 border-current transparent bg-dark"
      >
    </label>
    <button
      @click="login"
      class="bg-turquoise-500 mb-3 text-white font-bold py-2 px-4 border-b-4 border-turquoise-700 rounded focus:outline-none"
    >
      Login
    </button>
    <h2 class="hz-line-text"><span>OR</span></h2>
    <button
      @click="$emit('toggle-login', false)"
      class="bg-gray-dark-500 text-turquoise-700 font-bold py-2 px-4 border border-turquoise-500 rounded focus:outline-none"
    >
      Sign up
    </button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        token: null,
        user: null,
      }
    },

    mounted() {
      this.focusInput()
    },

    methods: {
      focusInput() {
        this.$refs.token.focus()
      },
      login() {
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
.bg-turquoise-500 {
  background-color: #00b6ca;
}

.bg-gray-dark-500 {
  background-color: #495057;
}

.bg-gray-dark-500:hover {
  background-color: #545C64;
}

.bg-turquoise-500:hover {
  background-color: #00CAE0;
}

.text-turquoise-700 {
  color: #00b6ca;
}

.border-turquoise-700 {
  border-color: #00818F;
}

.border-turquoise-500 {
  border-color: #00b6ca;
}

.border-turquoise-700:hover {
  border-color: #00A5B8;
}

.bg-dark {
  background-color: #393e46;
}

.border-b:focus {
  border-bottom-width: 2px;
}

.container h2.hz-line-text {
   width: 100%;
   text-align: center;
   border-bottom: 1px solid #00b6ca;
   line-height: 0.1em;
   margin: 10px 0 20px;
}

.container h2.hz-line-text span {
    background: #393e46;
    padding:0 10px;
}
</style>
