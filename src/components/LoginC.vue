<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
// import router from '@/router'

const emit = defineEmits(['forgot', 'signup'])

const email = ref('')
const password = ref('')
const wrongData = ref(false)

const doLogin = () => {
  axios
    .post('http://localhost:8080/api/auth/login', {
      email: email.value,
      password: password.value
    })
    .then((response) => {
      console.log(response)
      localStorage.setItem('token', response.data.accessToken)
      localStorage.setItem('user', response.data.roles[0])
      window.location.reload()
    })
    .catch((error) => {
      console.log(error)
      wrongData.value = true
      setTimeout(() => {
        wrongData.value = false
      }, 3000)
    })
}
</script>

<template>
  <div class="login">
    <p class="login__title">Log in to your Course <span>Lab</span> account</p>
    <form @submit.prevent="doLogin" class="login__form">
      <div class="login__inputs-list">
        <input type="email" v-model="email" class="login__input" placeholder="Email" required />
        <input
          type="password"
          v-model="password"
          class="login__input"
          placeholder="Password"
          required
        />
      </div>
      <button type="submit" class="login__submit">Log in</button>
      <p class="wrong-password" v-if="wrongData">Wrong password or email</p>
    </form>
    <div class="login__other">
      <!-- <p class="login__other-forget">or <span @click="emit('forgot')">Forgot Password</span></p> -->
      <hr />
      <p class="login__other-signup">
        Don't have an account? <span @click="emit('signup')">Sign up</span>
      </p>
    </div>
  </div>
</template>

<style scoped lang="scss">
.wrong-password {
  color: #ff0000;
  font-weight: 700;
  font-size: 14px;
  margin-top: 16px;
  text-align: center;
  margin-bottom: -20px;
}
.login {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 47px 0 250px 0;
  width: 100%;
  max-width: 352px;
  margin: 0 auto;
}
.login__title {
  color: #e0e1e3;
  font-weight: 700;
  font-size: 16px;
  span {
    color: #5cdb95;
    font-weight: 700;
    font-size: 16px;
  }
}
.login__form {
  width: 100%;
}
.login__inputs-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 8px;
  margin-top: 34px;
  width: 100%;
  .login__input {
    color: #e0e1e3;
    font-weight: 700;
    font-size: 14px;
    padding: 21px 28px;
    border: 1px solid #5cdb95;
    border-radius: 30px;
    background: transparent;
    width: 100%;
  }
  .login__input::placeholder {
    color: #e0e1e3;
    font-weight: 700;
    font-size: 14px;
  }
}
.login__submit {
  color: #0d0d0d;
  padding: 13.41px 0;
  background: #5cdb95;
  border-radius: 30px;
  transition: all 0.3s ease;
  text-align: center;
  font-weight: 700;
  font-size: 16px;
  margin-top: 16px;
  width: 100%;
  border: none;
}
.login__submit:hover {
  background: #82fcb9;
}
.login__other {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 15px;
  margin-top: 25px;
  .login__other-forget {
    color: #ffffff;
    font-weight: 400;
    font-size: 16px;
    span {
      color: #5cdb95;
      font-weight: 700;
      font-size: 16px;
      transition: all 0.3s ease;
      text-decoration: underline;
      cursor: pointer;
    }
    span:hover {
      color: orange;
    }
  }
  hr {
    width: 100%;
    display: block;
    height: 2px;
    border: 0;
    border-top: 2px solid #2e363c;
    margin: 1em 0;
    padding: 0;
  }
  .login__other-signup {
    color: #ffffff;
    font-weight: 400;
    font-size: 14px;
    span {
      color: #5cdb95;
      font-weight: 700;
      font-size: 14px;
      transition: all 0.3s ease;
      text-decoration: underline;
      cursor: pointer;
    }
    span:hover {
      color: orange;
    }
  }
}
</style>
