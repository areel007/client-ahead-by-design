<template>
  <div class="register">
    <div class="container">
      <div class="register__inner">
        <form @submit.prevent="handleSubmit">

          <p class="form__title">Register</p>

          <p
            class="error-msg"
            v-if="!data.username.length>0 && !data.password.length>0"
          >
            {{ msg }}
          </p>

          <div class="form__control">
            <label>Username</label>
            <div class="box__input">
              <svg
                height="24px"
                viewBox="0 0 24 24"
                width="24px"
                fill="#000000"
              >
                <path d="M0 0h24v24H0V0z" fill="none"/>
                <path d="M12 6c1.1 0 2 .9 2 2s-.9 2-2 2-2-.9-2-2 .9-2 2-2m0 10c2.7
                0 5.8 1.29 6 2H6c.23-.72 3.31-2 6-2m0-12C9.79 4 8 5.79 8 8s1.79 4
                4 4 4-1.79 4-4-1.79-4-4-4zm0 10c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z"/>
              </svg>
              <input type="text" v-model="data.username">
            </div>
          </div>

            <div class="form__control">
              <label>Password</label>
              <div class="box__input">
                <svg height="24px"
                  viewBox="0 0 24 24"
                  width="24px" fill="#000000"
                >
                  <g fill="none"
                  >
                    <path d="M0 0h24v24H0V0z"/>
                    <path d="M0 0h24v24H0V0z" opacity=".87"/>
                  </g>
                  <path d="M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9
                  2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zM9 6c0-1.66 1.34-3 3-3s3 1.34
                  3 3v2H9V6zm9 14H6V10h12v10zm-6-3c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2z"/>
                </svg>
                <input :type="passwordType" v-model="data.password">
                <svg
                  height="24px"
                  viewBox="0 0 24 24"
                  width="24px" fill="#000000"
                  class="eye"
                  @click="togglePassword"
                  v-if="data.password.length>0"
                >
                  <path d="M0 0h24v24H0V0z" fill="none"/>
                  <path d="M12 6c3.79 0 7.17 2.13 8.82 5.5C19.17 14.87 15.79 17 12 17s-7.17-2.13-8.82-5.5C4.83
                  8.13 8.21 6 12 6m0-2C7 4 2.73 7.11 1 11.5 2.73 15.89 7 19 12 19s9.27-3.11 11-7.5C21.27
                  7.11 17 4 12 4zm0 5c1.38 0 2.5 1.12 2.5 2.5S13.38 14 12 14s-2.5-1.12-2.5-2.5S10.62 9
                  12 9m0-2c-2.48 0-4.5 2.02-4.5 4.5S9.52 16 12 16s4.5-2.02 4.5-4.5S14.48 7 12 7z"/>
                </svg>

              </div>
            </div>

          <p class="switch">Already have an account? <span @click="$router.push('/login')">Login</span></p>

            <button>Register</button>

        </form>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, reactive, ref} from "vue";
import { useRouter } from "vue-router";

import axios from "axios";

export default defineComponent({
  name: "register",
  setup(props, $router) {

    const router = useRouter()

    const data = reactive(
      {
        username: "",
        password: "",
      }
    )

    const msg = ref("")

    const passwordType = ref("password")

    /** Methods */
    const togglePassword = () => {
      if (passwordType.value === "password") {
        passwordType.value = "text"
      } else {
        passwordType.value = "password"
      }
    }

    const handleSubmit = async () => {
      if (data.username.trim() ==='' || data.password.trim() ==='') return
      try {
        await axios.post('http://localhost:4000/users/register', data)

      } catch (e) {
        console.log(e)
      }
      data.username = ""
      data.password = ""
    }

    return {
      data,
      passwordType,
      togglePassword,
      handleSubmit,
      msg,
    }
  }
});
</script>

<style scoped>
.register {
  position: relative;
  top: 50px;
}
.register__inner {
  width: 100%;
  position: relative;
}
.register__inner form {
  width: 30rem;
  position: relative;
  margin: 5rem auto;
}
.form__title {
  font-size: var(--fs-20);
  margin-bottom: 2rem;
}
.form__control {
  margin-bottom: 1rem;
}
.form__control label {
  font-size: 1.2rem;
}
.box__input {
  margin-top: .5rem;
  display: flex;
  align-items: center;
  border: 1px solid grey;
  padding: 0 .5rem;
}
.box__input svg {
  width: 1.8rem;
  height: 1.8rem;
}
.box__input input {
  padding: .5rem;
  width: 100%;
  outline: none;
  border: none;
}
form button {
  width: 10rem;
  padding: .5rem;
  cursor: pointer;
  outline: none;
  border: none;
  background-color: #0e0e0e;
  color: #fff;
}
.switch {
  margin-bottom: 1rem;
  font-size: 1.1rem;
}
.switch span {
  color: var(--secondary-color);
  cursor: pointer;
}
.eye {
  cursor: pointer;
}
.error-msg {
  font-size: 1.2rem;
  color: var(--secondary-color);
  margin-bottom: 1rem;
}
</style>
