<script setup lang="ts">
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
const router = useRouter()
const route = useRoute()

const emit = defineEmits(['signup', 'login'])
const token = localStorage.getItem('token')

const searchValue = ref('')
const doSearch = () => {
  console.log('search: ' + searchValue.value)
  searchValue.value = ''
}

const login = ref(false)
const signup = ref(false)
const showProfile = ref(false)

const goHome = () => {
  router.push('/')
  login.value = false
  signup.value = false
}

const goCourses = () => {
  router.push('/courses')
  login.value = false
  signup.value = false
}

const goProfile = () => {
  if (localStorage.getItem('token') === null) {
    router.push('/auth')
    login.value = true
    signup.value = false
  } else {
    showProfile.value = true
    login.value = false
    signup.value = false
  }
}

const toggleLogin = () => {
  if (route.path !== '/auth') {
    router.push('/auth')
  }
  login.value = true
  signup.value = false
  emit('login')
}

// const toggleSignup = () => {
//   signup.value = true
//   login.value = false
//   emit('signup')
// }

const logout = () => {
  localStorage.clear()
  router.push('/auth')
  login.value = false
  signup.value = false
  showProfile.value = false
}

const fullName = localStorage.getItem('fullName')
const email = localStorage.getItem('email')
</script>

<template>
  <div class="full-header-bg">
    <div class="container">
      <div class="header">
        <img src="/img/logo.png" @click="goHome" class="header__logo" alt="" />
        <RouterLink to="/courses" @click="goCourses" class="header__my-courses"
          >All courses</RouterLink
        >
        <form @submit.prevent="doSearch" class="header__search-form">
          <input
            type="text"
            v-model="searchValue"
            placeholder="&#xF002;      Search for anything"
            class="header__search"
          />
          <input type="submit" hidden />
        </form>
        <img src="/img/profile_icon.png" @click="goProfile" class="header__profile" alt="" />
        <div class="profile-popup" v-if="showProfile">
          <img src="/img/userAva.png" alt="" />
          <p class="user-name">{{ fullName }}</p>
          <p class="user-email">{{ email }}</p>
          <hr />
          <div class="notification" @click="router.push('/my-courses')">
            <img src="/img/learning.png" alt="" />
            <p class="notification-text">My courses</p>
          </div>
          <p class="edit-profile" @click="router.push('/edit-profile')">Edit profile</p>
          <p class="logout-profile" @click="logout">Logout</p>
        </div>
        <button to="/courses" class="header__login" @click="toggleLogin" v-if="!token">
          Log in
        </button>
        <!-- :class="{ 'header__auth-active': login }" -->

        <button
          to="/about"
          class="header__login header__auth-active about"
          @click="router.push('/about')"
        >
          About us
        </button>
      </div>
    </div>
  </div>
  <div v-if="showProfile" @click="showProfile = false" class="cover_dark"></div>
</template>

<style scoped lang="scss">
.full-header-bg {
  background: #0d0d0d;
  width: 100%;
}
.header {
  display: flex;
  align-items: center;
  padding: 25px 26px;
  background: #0d0d0d;
}
.header__logo {
  cursor: pointer;
}
.header__my-courses {
  color: #000000;
  font-weight: 700;
  font-size: 14px;
  line-height: 17px;
  padding: 10px 20px;
  background: #5cdb95;
  border-radius: 30px;
  transition: all 0.3s ease;
  margin: 0 30px;
  white-space: nowrap;
}

.header__search-form {
  width: 100%;
}
.header__search {
  font-family: 'Roboto', FontAwesome;
  color: #5cdb95;
  padding: 15px 20px;
  background: #131313;
  border: 1px solid #5cdb95;
  border-radius: 9999px;
  font-weight: 400;
  font-size: 14px;
  width: 100%;
}
.header__search::placeholder {
  color: #5cdb95;
  font-weight: 400;
  font-size: 14px;
}
.header__profile {
  margin: 0 20px 0 30px;
  cursor: pointer;
}
.profile-popup {
  position: absolute;
  padding: 37px 46px;
  background: #ffffff;
  box-shadow: 0px 8px 32px rgba(0, 0, 0, 0.06);
  border-radius: 20px;
  z-index: 10;
  right: 70px;
  top: 75px;
  text-align: center;
}
.cover_dark {
  background: #000000;
  opacity: 0.5;
  z-index: 9;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
}
.user-name {
  font-weight: 500;
  font-size: 20px;
  color: #202020;
  margin-top: 10px;
}
.user-email {
  font-weight: 275;
  font-size: 13px;
  color: #202020;
}

hr {
  width: 250px;
  margin-top: 10px;
  border-top: 2px solid #dcdbdd;
}

.notification {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-top: 24px;
  cursor: pointer;
}

.notification img {
  width: 24px;
  height: 24px;
}

.notification-text {
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  color: #202020;
}

.notification:hover .notification-text {
  transition: all 0.3s ease-out;
  text-decoration: underline;
  text-underline-offset: 5px;
  text-decoration-thickness: 2px;
}

.edit-profile {
  font-weight: 500;
  font-size: 15px;
  color: #ffffff;
  padding: 8px 0px;
  width: 100%;
  max-width: 155px;
  background: #009580;
  border-radius: 12px;
  margin: 0 auto;
  margin-top: 25px;
  cursor: pointer;
  transition: all 0.3s ease-out;
}

.edit-profile:hover {
  background: #035a4e;
}

.logout-profile {
  font-weight: 500;
  font-size: 15px;
  color: #ffffff;
  padding: 8px 0px;
  width: 100%;
  max-width: 155px;
  background: #aa2020;
  border-radius: 12px;
  margin: 0 auto;
  margin-top: 10px;
  cursor: pointer;
  transition: all 0.3s ease-out;
}

.logout-profile:hover {
  background: #8b0101;
}
.header__login,
.header__signup {
  color: #5cdb95;
  font-weight: 700;
  font-size: 14px;
  padding: 12px 16px;
  border: 1px solid #5cdb95;
  border-radius: 30px;
  background: #0d0d0d;
  margin-right: 8px;
  transition: all 0.3s ease;
  white-space: nowrap;
}
.header__login:hover,
.header__signup:hover {
  background: #5cdb95;
  color: #0d0d0d;
}
.header__auth-active {
  font-weight: 700;
  font-size: 14px;
  color: #0d0d0d;
  padding: 12px 16px;
  background: #5cdb95;
  border-radius: 30px;
  white-space: nowrap;
}

.header__my-courses:hover,
.about:hover {
  background: #00ad4e;

  color: white;
}
</style>
