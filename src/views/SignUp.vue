<template>
  <div>
    <Header />
    <div class="flex items-center justify-center px-4 py-12 sm:px-6 lg:px-8">
      <div class="w-2/5 space-y-8 border-2 p-11">
        <div>
          <h2 class="mt-6 text-3xl font-extrabold text-center text-gray-900">
            Sign Up
          </h2>
          <p class="mt-2 text-sm text-center text-gray-600"></p>
        </div>
        <form
          @submit.prevent="Register"
          class="mt-8 space-y-6"
          action="#"
          method="POST"
        >
          <div class="-space-y-px rounded-md shadow-sm">
            <div>
              <input
                type="email"
                v-model="user.email"
                autocomplete="email"
                required
                class="relative block w-full px-3 py-2 text-gray-900 placeholder-gray-500 border border-gray-300 rounded-none appearance-none rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
                placeholder="Email address"
              />
            </div>
            <div>
              <input
                type="password"
                v-model="user.password"
                autocomplete="current-password"
                required
                class="relative block w-full px-3 py-2 text-gray-900 placeholder-gray-500 border border-gray-300 rounded-none appearance-none rounded-b-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm"
                placeholder="Password"
              />
            </div>
          </div>
          <div class="flex items-center justify-between">
            <div class="flex items-center">
              <input
                id="remember_me"
                name="remember_me"
                type="checkbox"
                class="w-4 h-4 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500"
              />
              <label for="remember_me" class="block ml-2 text-sm text-gray-900">
                Remember me
              </label>
            </div>
          </div>
          <div>
            <button
              @click="createUser"
              type="submit"
              class="relative flex justify-center w-full px-4 py-2 text-sm font-medium text-white bg-indigo-600 border border-transparent rounded-md group hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              <span class="absolute inset-y-0 left-0 flex items-center pl-3">
                <svg
                  class="w-5 h-5 text-indigo-500 group-hover:text-indigo-400"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                  aria-hidden="true"
                >
                  <path
                    fill-rule="evenodd"
                    d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z"
                    clip-rule="evenodd"
                  />
                </svg>
              </span>
              Sign Up
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import Header from '../components/Header'
import firebase from 'firebase'
export default {
  components: { Header },
  data() {
    return {
      user: {
        email: '',
        password: '',
      },
      submitted: false,
    }
  },
  methods: {
    createUser() {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.user.email, this.user.password)
        .then((res) => {
          console.log(res)
        })
        .catch(function(error) {
          var errorCode = error.code
          var errorMessage = error.message
          console.log(errorCode, errorMessage)
        })
    },
    Register(e) {
      this.submitted = true
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.user.email, this.user.password)
        .then(() => {
          alert('well done ! your new account has been created')
        })
      alert('SUCCESS!!:-)' + JSON.stringify(this.user))
      this.$router.push('/')
    },
  },
}
</script>
