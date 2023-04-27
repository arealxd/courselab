<script setup lang="ts">
import HeaderC from '@/components/HeaderC.vue'
import FooterC from '@/components/FooterC.vue'
import { ref } from 'vue'
import { useRouter } from 'vue-router'
const router = useRouter()
import coursesJson from '@/json/courses.json'

const courses = ref(coursesJson)

const firstIndex = ref(0)
const secondIndex = ref(1)
const thirdIndex = ref(2)
const fourthIndex = ref(3)

const nextCourse = () => {
  if (thirdIndex.value === courses.value.length - 1) {
    firstIndex.value = 0
    secondIndex.value = 1
    thirdIndex.value = 2
    fourthIndex.value = 3
  } else {
    firstIndex.value++
    secondIndex.value++
    thirdIndex.value++
    fourthIndex.value++
  }
}

const previousCourse = () => {
  if (firstIndex.value === 0) {
    firstIndex.value = courses.value.length - 4
    secondIndex.value = courses.value.length - 3
    thirdIndex.value = courses.value.length - 2
    fourthIndex.value = courses.value.length - 1
  } else {
    firstIndex.value--
    secondIndex.value--
    thirdIndex.value--
    fourthIndex.value--
  }
}

window.scrollTo(0, 0)
</script>

<template>
  <HeaderC />
  <div class="container">
    <div class="hero">
      <div class="hero__content">
        <p class="hero__content__title">
          What is the difference between the project and other educational platforms?
        </p>
        <p class="hero__content-description">
          Payment per student (the course is bought by 5 people for a month, so pay only for 5 and
          do not need to overpay, that is, the task of helping people to promote their learning and
          not to spend a large amount)
        </p>
        <button class="hero__content-getstarted" @click="router.push('/courses')">
          Get started
        </button>
        <div class="hero__content-statistics">
          <div class="statistics__content">
            <p>20M</p>
            <P>Finished</P>
          </div>
          <div class="statistics__content">
            <p>50M</p>
            <P>Students</P>
          </div>
        </div>
      </div>
      <img class="hero__img" src="/img/hero_image.png" alt="" />
    </div>
    <div class="rec">
      <p class="rec__title">Recommended Courses</p>
      <p class="rec__description">
        Choose the online video course you need, new additions are published every month.
      </p>
      <div class="rec__list">
        <img @click="previousCourse" src="/img/button-left.png" class="arrow" alt="" />
        <div class="rec__courses">
          <div class="course" @click="router.push('/details/' + courses[firstIndex].id + '/' + 3)">
            <img :src="courses[firstIndex].image" alt="" />
            <p class="course__name">{{ courses[firstIndex].title }}</p>
            <p class="course__author">{{ courses[firstIndex].author }}</p>
          </div>
          <div class="course" @click="router.push('/details/' + courses[secondIndex].id + '/' + 3)">
            <img :src="courses[secondIndex].image" alt="" />
            <p class="course__name">{{ courses[secondIndex].title }}</p>
            <p class="course__author">{{ courses[secondIndex].author }}</p>
          </div>
          <div class="course" @click="router.push('/details/' + courses[thirdIndex].id + '/' + 3)">
            <img :src="courses[thirdIndex].image" alt="" />
            <p class="course__name">{{ courses[thirdIndex].title }}</p>
            <p class="course__author">{{ courses[thirdIndex].author }}</p>
          </div>
          <div class="course" @click="router.push('/details/' + courses[fourthIndex].id + '/' + 3)">
            <img :src="courses[fourthIndex].image" alt="" />
            <p class="course__name">{{ courses[fourthIndex].title }}</p>
            <p class="course__author">{{ courses[fourthIndex].author }}</p>
          </div>
        </div>
        <img @click="nextCourse" src="/img/button-left.png" class="arrow arrow-rotate" alt="" />
      </div>
    </div>
  </div>
  <FooterC />
</template>

<style scoped lang="scss">
.hero {
  padding: 40px 60px 40px 145px;
  background: #383535;
  border-radius: 24.6857px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
}
.hero__content {
  display: flex;
  flex-direction: column;
}
.hero__content__title {
  font-weight: 700;
  font-size: 50px;
  line-height: 1;
  color: #5cdb95;
  max-width: 700px;
}
.hero__content-description {
  font-weight: 400;
  font-size: 22px;
  line-height: 28px;
  color: #dddddd;
  max-width: 662px;
  margin-top: 15px;
  margin-bottom: 25px;
}

.hero__img {
  max-width: 650px;
}
.hero__content-getstarted {
  padding: 15px 48px;
  font-weight: 500;
  font-size: 20px;
  color: #202020;
  background: #5cdb95;
  box-shadow: 8.22857px 8.22857px 43.8857px rgba(32, 119, 110, 0.21);
  border-radius: 34.2857px;
  transition: all 0.3s ease;
  max-width: 207.7px;
}
.hero__content-getstarted:hover {
  background: #009719;
  color: white;
}
.hero__content-statistics {
  margin-top: 53px;
  display: flex;
  align-items: center;
  gap: 67px;
}
.statistics__content {
  display: flex;
  flex-direction: column;
  gap: 0px;
  :nth-child(1) {
    font-weight: 700;
    font-size: 41px;
    color: #ffffff;
    line-height: 1;
  }
  :nth-child(2) {
    font-weight: 400;
    font-size: 24px;
    color: #ffffff;
  }
}
.rec {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 60px 145px 150px 145px;
  .rec__title {
    font-weight: 700;
    font-size: 30px;
    color: #e0e1e3;
  }
  .rec__description {
    font-weight: 400;
    font-size: 20px;
    color: #e0e1e3;
  }
  .rec__list {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 30px;
  }
  .arrow {
    cursor: pointer;
  }
  .arrow-rotate {
    transform: rotate(180deg);
  }
  .rec__courses {
    display: flex;
    align-items: center;
    width: 100%;
    gap: 10px;
    justify-content: space-around;
    padding: 0px 20px;
  }
  .course {
    display: flex;
    flex-direction: column;
    cursor: pointer;
    img {
      width: 230px;
      height: 130px;
      border-radius: 20px;
    }
    .course__name {
      font-weight: 700;
      font-size: 16px;
      color: #e0e1e3;
      margin-top: 8px;
      margin-bottom: 3px;
    }
    .course__author {
      font-weight: 400;
      font-size: 11px;
      display: flex;
      color: #6a6f73;
    }
  }
}
</style>
