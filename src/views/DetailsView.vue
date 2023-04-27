<script setup lang="ts">
import HeaderC from '@/components/HeaderC.vue'
import FooterC from '@/components/FooterC.vue'
import { ref } from 'vue'
import { useRouter } from 'vue-router'
const router = useRouter()
import { useRoute } from 'vue-router'
import coursesJson from '@/json/courses.json'

const route = useRoute()
const course = ref(coursesJson.find((course) => course.id == route.params.id))

window.scrollTo(0, 0)
</script>

<template>
  <HeaderC />
  <div class="container">
    <div class="courses">
      <div class="courses__breadcrumbs">
        <p @click="router.push('/')">Home</p>
        <svg
          width="7"
          height="12"
          viewBox="0 0 7 12"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M-1.34741 1.41L3.23259 6L-1.34741 10.59L0.0625877 12L6.06259 6L0.0625877 0L-1.34741 1.41Z"
            fill="white"
          />
        </svg>
        <p v-if="route.params.from == 1" @click="router.push('/my-courses')">My courses</p>
        <p v-else-if="route.params.from == 2" @click="router.push('/courses')">Courses</p>
        <p v-else-if="route.params.from == 3">{{ course.title }}</p>
        <p v-else>Courses</p>
        <svg
          v-if="route.params.from != 3"
          width="7"
          height="12"
          viewBox="0 0 7 12"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M-1.34741 1.41L3.23259 6L-1.34741 10.59L0.0625877 12L6.06259 6L0.0625877 0L-1.34741 1.41Z"
            fill="white"
          />
        </svg>
        <p v-if="route.params.from != 3">{{ course.title }}</p>
      </div>
      <div class="courses__preview">
        <div class="courses__preview-img">
          <img :src="course.image" alt="" />
          <div class="courses__preview-info-btns">
            <button class="courses__preview-info-btns-buy">Buy now</button>
          </div>
        </div>
        <div class="courses__preview-info">
          <div class="courses__preview-header">
            <p class="courses__preview-info-title">{{ course.title }}</p>

            <p class="price">{{ course.price }} $</p>
          </div>
          <p class="author">
            Author: <span>{{ course.author }}</span>
          </p>
          <p class="language">
            Language: <span>{{ course.courseLanguage }}</span>
          </p>
          <div class="hours">
            <p>{{ course.totalHours }} total hours</p>
            <svg
              width="6"
              height="6"
              viewBox="0 0 6 6"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M2.79138 5.37588C4.11138 5.37588 5.16738 4.31987 5.16738 2.99987C5.16738 1.67987 4.11138 0.623875 2.79138 0.623875C1.47138 0.623875 0.415375 1.67987 0.415375 2.99987C0.415375 4.31987 1.47138 5.37588 2.79138 5.37588Z"
                fill="#6A6F73"
              />
            </svg>

            <p>{{ course.lecturesQuantity }} lectures</p>
          </div>
          <div class="rating">
            <img src="/img/star.png" alt="" />
            <p>{{ course.rating }}</p>
          </div>
          <p class="courses__preview-info-desc">{{ course.description }}</p>
        </div>
      </div>
    </div>
  </div>
  <FooterC />
</template>

<style scoped lang="scss">
.courses {
  padding: 30px 150px 0px 150px;
  padding-bottom: 200px;
  display: flex;
  flex-direction: column;
  background: #383535;
  border-radius: 30px;
  margin-bottom: 30px;
}
.courses__breadcrumbs {
  display: flex;
  align-items: center;
  gap: 10px;
  p {
    font-weight: 700;
    font-size: 14px;
  }
}
.courses__preview {
  display: flex;
  gap: 30px;
  margin-top: 30px;
  .courses__preview-img {
    width: 400px;
    height: 400px;
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 30px;
    }
    .courses__preview-info-btns {
      margin-top: 20px;

      .courses__preview-info-btns-buy {
        width: 100%;
        padding: 15px 0px;
        background: #5cdb95;
        border-radius: 30px;
        border: none;
        font-weight: 700;
        font-size: 18px;
        color: #000000;
        cursor: pointer;
        transition: all 0.3s ease;
      }
      .courses__preview-info-btns-buy:hover {
        background: #4ea884;
      }
    }
  }
  .courses__preview-info {
    display: flex;
    flex-direction: column;
    gap: 10px;
    .courses__preview-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      .price {
        font-weight: 700;
        font-size: 25px;
        color: #1ae200;
      }
    }
    .courses__preview-info-title {
      font-weight: 700;
      font-size: 30px;
      color: #ffffff;
    }
    .courses__preview-info-desc {
      font-weight: 400;
      font-size: 18px;
      color: #ffffff;
      max-width: 867px;
    }
  }
  .author {
    font-weight: 400;
    font-size: 14px;
    color: #c9c9c9;
    span {
      font-weight: 700;
      font-size: 14px;
      color: #c9c9c9;
    }
  }
  .language {
    font-weight: 400;
    font-size: 14px;
    color: #ffffff;
    span {
      font-weight: 700;
      font-size: 14px;
      color: #fdff87;
    }
  }
  .hours {
    display: flex;
    align-items: center;
    gap: 10px;
    p {
      font-weight: 500;
      font-size: 13px;
      color: #cbcbcb;
    }
  }
  .rating {
    display: flex;
    align-items: center;
    gap: 10px;
    img {
      width: 15px;
      height: 15px;
    }
    p {
      font-weight: 700;
      font-size: 16px;
      color: #f0c800;
    }
  }
}
</style>
