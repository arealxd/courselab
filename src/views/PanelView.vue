<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const admin = ref(true)

const activeAdminNav = ref(0)
const activeTeacherNav = ref(0)
const successCreated = ref(false)

const fullName = ref('')
const dateOfBirth = ref('')
const email = ref('')
const password = ref('')

const caterogyName = ref('')

const caterogyId = ref('')
const tagName = ref('')

const createTeacher = () => {
  successCreated.value = true
  setTimeout(() => {
    successCreated.value = false
    fullName.value = ''
    dateOfBirth.value = ''
    email.value = ''
    password.value = ''
  }, 3000)
}

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

const createCategory = () => {
  successCreated.value = true
  setTimeout(() => {
    successCreated.value = false
    caterogyName.value = ''
  }, 3000)
}

const createTag = () => {
  successCreated.value = true
  setTimeout(() => {
    successCreated.value = false
    caterogyId.value = ''
    tagName.value = ''
  }, 3000)
}

const doLogout = () => {
  // localStorage.clear()
  router.push('/')
}
</script>

<template>
  <div class="background">
    <div class="header-out">
      <div class="container">
        <div class="header-in">
          <img src="/img/logo-panel.svg" alt="" />
          <div class="header__role" @click="admin = true" v-if="!admin">
            <img src="/img/teacher.png" alt="" />
            <p>Teacher panel</p>
          </div>
          <div class="header__role" @click="admin = false" v-else>
            <img src="/img/admin.png" alt="" />
            <p>Admin panel</p>
          </div>
        </div>
      </div>
    </div>
    <div class="container create">
      <div class="create__nav" v-if="admin">
        <button :class="{ active: activeAdminNav === 0 }" @click="activeAdminNav = 0">
          Create teacher
        </button>
        <button :class="{ active: activeAdminNav === 1 }" @click="activeAdminNav = 1">
          Get all teachers
        </button>
        <button :class="{ active: activeAdminNav === 2 }" @click="activeAdminNav = 2">
          Create category
        </button>
        <button :class="{ active: activeAdminNav === 3 }" @click="activeAdminNav = 3">
          Create tag
        </button>
        <button class="logout" @click="doLogout">Logout</button>
      </div>
      <div class="create__nav" v-else>
        <button :class="{ active: activeTeacherNav === 0 }" @click="activeTeacherNav = 0">
          Create course
        </button>
        <button :class="{ active: activeTeacherNav === 1 }" @click="activeTeacherNav = 1">
          Update course
        </button>
        <button :class="{ active: activeTeacherNav === 2 }" @click="activeTeacherNav = 2">
          Delete course by ID
        </button>
      </div>
      <form
        @submit.prevent="createTeacher"
        class="create__create-teacher"
        v-if="activeAdminNav === 0 && admin"
      >
        <input v-model="fullName" type="text" placeholder="Full name" required />
        <input
          v-model="dateOfBirth"
          @input="onDateInput"
          type="text"
          placeholder="Date of birth"
          required
        />
        <input v-model="email" type="email" placeholder="Email" required />
        <input v-model="password" type="password" placeholder="Password" required />
        <button type="submit">Create</button>
        <p class="success-created" v-if="successCreated">Teacher created</p>
      </form>
      <div class="create__get-teachers" v-if="activeAdminNav === 1 && admin">
        <div class="create__get-teachers__teacher header-teacher">
          <p class="create__get-teachers__teacher__name">ID</p>
          <p class="create__get-teachers__teacher__email">Full name</p>
          <p class="create__get-teachers__teacher__date">Email</p>
          <p class="create__get-teachers__teacher__date">Date of birth</p>
        </div>
        <div class="teachers-table">
          <div class="create__get-teachers__teacher" v-for="teacher in 10" :key="teacher">
            <p class="create__get-teachers__teacher__name">1</p>
            <p class="create__get-teachers__teacher__email">Gulfairuz Akhan</p>
            <p class="create__get-teachers__teacher__date">gufa@mail.ru</p>
            <p class="create__get-teachers__teacher__date">07.31.2002</p>
          </div>
        </div>
      </div>
      <form
        @submit.prevent="createCategory"
        class="create__create-teacher"
        v-if="activeAdminNav === 2 && admin"
      >
        <input v-model="caterogyName" type="text" placeholder="Category name" required />
        <button type="submit">Create</button>
        <p class="success-created" v-if="successCreated">Category created</p>
      </form>
      <form
        @submit.prevent="createTag"
        class="create__create-teacher"
        v-if="activeAdminNav === 3 && admin"
      >
        <input v-model="caterogyId" type="text" placeholder="Category ID" required />
        <input v-model="tagName" type="text" placeholder="Tag name" required />
        <button type="submit">Create</button>
        <p class="success-created" v-if="successCreated">Tag created</p>
      </form>
    </div>
  </div>
</template>

<style scoped lang="scss">
.background {
  height: 100vh;
  width: 100vw;
  background-color: #ffffff;
}
.header-out {
  width: 100%;
  background: #2a3042;
}
.header-in {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  padding: 30px 0px;
  gap: 30px;
  .header__role {
    display: flex;
    align-items: center;
    gap: 15px;
    img {
      width: 30px;
      height: 30px;
    }
    p {
      font-weight: 700;
      font-size: 20px;
      color: #c3c0c0;
    }
  }
}
.create {
  padding-bottom: 200px;
  background: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 40px;
  .create__nav {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 35px;
    button {
      padding: 10px 30px;
      background: #007bff;
      border-radius: 30px;
      font-weight: 700;
      font-size: 16px;
      color: #ffffff;
      border: none;
      cursor: pointer;
      transition: all 0.3s ease;
      &:hover {
        background: #005bbc;
      }
    }
    .active {
      background: #1bb600;
      &:hover {
        background: #1bb600;
      }
    }
    .logout {
      padding: 10px 30px;
      background: #e70000;
      border-radius: 30px;
      font-weight: 700;
      font-size: 16px;
      color: #ffffff;
      border: none;
      cursor: pointer;
      transition: all 0.3s ease;
      &:hover {
        background: #c50000;
      }
    }
  }
}
.create__create-teacher {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  input {
    width: 300px;
    height: 40px;
    border: 1px solid #c3c0c0;
    border-radius: 30px;
    padding: 0px 20px;
    font-weight: 700;
    font-size: 16px;
    color: #383838;
    outline: none;
    transition: all 0.3s ease;
    &:focus {
      border: 1px solid #007bff;
    }
  }
  button {
    width: 100%;
    max-width: 300px;
    padding: 10px 30px;
    border: none;
    border-radius: 30px;
    background: #007bff;
    font-weight: 700;
    font-size: 16px;
    color: #ffffff;
    cursor: pointer;
    transition: all 0.3s ease;
    &:hover {
      background: #005bbc;
    }
  }
}
.create__get-teachers {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  width: 100%;
  max-width: 700px;
  .teachers-table {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 15px;
    width: 100%;
    max-width: 700px;
    // overflow-y: auto;
    // height: 100%;
    // max-height: 300px;
  }
  .create__get-teachers__teacher {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    max-width: 700px;
    padding: 10px 30px;
    border: 1px solid #c3c0c0;
    border-radius: 10px;
    background: #ffffff;
    font-weight: 700;
    font-size: 16px;
    color: #383838;
    cursor: pointer;
    transition: all 0.3s ease;
    &:hover {
      background: #f2f2f2;
    }
    .create__get-teachers__teacher__name {
      font-weight: 700;
      font-size: 16px;
      color: #383838;
    }
    .create__get-teachers__teacher__email {
      font-weight: 400;
      font-size: 16px;
      color: #383838;
    }
    .create__get-teachers__teacher__date {
      font-weight: 400;
      font-size: 16px;
      color: #383838;
    }
  }
  .header-teacher {
    background: #2a3042;
    border: 1px solid #2a3042;
    .create__get-teachers__teacher__name {
      color: #ffffff;
    }
    .create__get-teachers__teacher__email {
      color: #ffffff;
    }
    .create__get-teachers__teacher__date {
      color: #ffffff;
    }
    &:hover {
      background: #2a3042;
    }
  }
}

.success-created {
  color: #1bb600;
  font-weight: 700;
  font-size: 16px;
  margin-top: -5px;
}
.error-text {
  color: #e70000;
  font-weight: 700;
  font-size: 16px;
  margin-top: -5px;
}
</style>
