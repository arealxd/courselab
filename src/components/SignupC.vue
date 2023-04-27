<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

const emit = defineEmits(['forgot', 'login'])
const fullName = ref('')
const dateOfBirth = ref('')
const email = ref('')
const password = ref('')

const onDateInput = (event: any) => {
  // Remove non-numeric characters from the input
  const cleanedInput = event.target.value.replace(/\D/g, '')
  // Format the input as a date (DD/MM/YYYY)
  if (cleanedInput.length <= 2) {
    dateOfBirth.value = cleanedInput
  } else if (cleanedInput.length <= 4) {
    dateOfBirth.value = cleanedInput.slice(0, 2) + '/' + cleanedInput.slice(2)
  } else {
    dateOfBirth.value =
      cleanedInput.slice(0, 2) + '/' + cleanedInput.slice(2, 4) + '/' + cleanedInput.slice(4, 8)
  }
}

const doSignup = () => {
  axios
    .post('http://localhost:8080/api/auth/register', {
      fullName: fullName.value,
      dateOfBirth: dateOfBirth.value,
      email: email.value,
      password: password.value,
      matchingPassword: password.value
    })
    .then((response) => {
      console.log(response)
    })
    .catch((error) => {
      console.log(error)
    })
}
</script>

<template>
  <div class="login">
    <p class="login__title">Sign up and start learning</p>
    <form @submit.prevent="doSignup" class="login__form">
      <div class="login__inputs-list">
        <input
          type="text"
          v-model="fullName"
          class="login__input"
          placeholder="Full name"
          required
        />
        <input
          type="text"
          v-model="dateOfBirth"
          @input="onDateInput"
          class="login__input"
          placeholder="Date of birth"
          required
        />
        <input type="email" v-model="email" class="login__input" placeholder="Email" required />
        <input
          type="password"
          v-model="password"
          class="login__input"
          placeholder="Password"
          required
        />
      </div>
      <button type="submit" class="login__submit">Sign up</button>
    </form>
    <div class="login__other">
      <!-- <p class="login__other-forget">or <span @click="emit('forgot')">Forgot Password</span></p> -->
      <hr />
      <p class="login__other-signup">
        Already have an account? <span @click="emit('login')">Log in</span>
      </p>
    </div>
  </div>
</template>

<style scoped lang="scss">
.login {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 47px 0 202px 0;
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
