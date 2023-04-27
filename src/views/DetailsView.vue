<script setup lang="ts">
import HeaderC from '@/components/HeaderC.vue'
import FooterC from '@/components/FooterC.vue'
import { ref } from 'vue'
import { useRouter } from 'vue-router'
const router = useRouter()
import { useRoute } from 'vue-router'
import coursesJson from '@/json/courses.json'
import VideoPopup from '@/components/VideoPopup.vue'

const route = useRoute()
const course = ref(coursesJson.find((course) => course.id == route.params.id))

window.scrollTo(0, 0)

const buyed = ref(false)

const buyForm = ref(false)
const successBuy = ref(false)

const buy_post = () => {
  successBuy.value = true
  setTimeout(() => {
    buyed.value = true
    buyForm.value = false
  }, 2000)
}

const showPopup = ref(false)
</script>

<template>
  <HeaderC />
  <div class="container">
    <div class="courses" :class="{ 'unset-padding': buyed }">
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
            <button
              class="courses__preview-info-btns-buy"
              type="button"
              @click="buyForm = true"
              v-if="!buyForm && !buyed"
            >
              Buy now
            </button>
            <form @submit.prevent="buy_post" v-if="buyForm" class="buy-form">
              <div class="form-inputs">
                <input type="text" class="buy-form__num" required placeholder="Card number" />
                <input type="text" class="buy-form__date" required placeholder="Expiration date" />
                <input type="text" class="buy-form__cvv" required placeholder="CVV" />
              </div>
              <div class="form-inputs">
                <input type="text" class="buy-form__num owner" required placeholder="Owner" />
                <img src="/img/visa.png" alt="" />
              </div>
              <button class="courses__preview-info-btns-buy" type="submit" style="margin-top: 15px">
                Buy now
              </button>
              <p class="success_buy" v-if="successBuy">Purchased successfully</p>
            </form>
          </div>
        </div>
        <div class="courses__preview-info">
          <div class="courses__preview-header">
            <p class="courses__preview-info-title">{{ course.title }}</p>

            <p class="price" v-if="!buyed">{{ course.price }} $</p>
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
    <div class="content">
      <div class="content__learn">
        <p class="content__learn-title">What you'll learn</p>
        <div class="content__learn-list">
          <div class="content__learn-list-item" v-for="i in 6" :key="i">
            <svg
              width="24"
              height="20"
              viewBox="0 0 24 20"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M8.99991 16.6232L4.82991 12.4532L3.40991 13.8632L8.99991 19.4532L20.9999 7.45315L19.5899 6.04315L8.99991 16.6232Z"
                fill="#E0E1E3"
              />
            </svg>
            <p>
              Pianoforte solicitude so decisively unpleasing conviction is partiality he. Or
              particular so diminution entreaties oh do. Real he me fond show gave shot plan. Mirth
              blush linen small hoped way its along.
            </p>
          </div>
        </div>
      </div>
      <p class="content__title">Course content</p>
      <div class="content__section" v-for="n in 5" :key="n">
        <div class="content__section-title">
          <p>{{ n }}. Object Oriented Programming</p>
          <p>4 lectures • 41min</p>
        </div>
        <div v-if="n === 1 || buyed">
          <div class="content__section-videos" v-for="i in 4" :key="i">
            <div class="content__section-videos-name">
              <svg
                width="15"
                height="13"
                viewBox="0 0 15 13"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M13.6364 0.59375H1.36364C0.606818 0.59375 0 1.20057 0 1.95739V10.1392C0 10.5009 0.143668 10.8477 0.3994 11.1034C0.655131 11.3592 1.00198 11.5028 1.36364 11.5028H4.77273V12.8665H10.2273V11.5028H13.6364C14.3864 11.5028 14.9932 10.8892 14.9932 10.1392L15 1.95739C15 1.59573 14.8563 1.24888 14.6006 0.99315C14.3449 0.737418 13.998 0.59375 13.6364 0.59375ZM13.6364 10.1392H1.36364V1.95739H13.6364V10.1392ZM10.2273 6.0483L5.45455 8.77557V3.32102L10.2273 6.0483Z"
                  fill="#E0E1E3"
                />
              </svg>
              <p @click="showPopup = true">Course Introduction</p>
            </div>
            <p class="content__section-videos-duration">06:39</p>
            <VideoPopup
              :videourl="'https://www.youtube.com/embed/nhBVL41-_Cw'"
              :onClose="
                () => {
                  showPopup = false
                }
              "
              v-if="showPopup"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
  <FooterC />
</template>

<style scoped lang="scss">
.courses {
  padding: 30px 0px 0px 150px;
  padding-bottom: 230px;
  display: flex;
  flex-direction: column;
  background: #383535;
  border-radius: 30px;
  margin-bottom: 40px;
}
.unset-padding {
  padding-bottom: 50px;
}
.courses__breadcrumbs {
  display: flex;
  align-items: center;
  gap: 10px;
  p {
    font-weight: 700;
    font-size: 14px;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  p:hover {
    color: #5cdb95;
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
.content {
  padding: 0px 150px 0px 150px;
  padding-bottom: 200px;
  .content__learn {
    padding: 25px;
    border: 1px solid #2e363c;
    border-radius: 30px;
    .content__learn-title {
      font-weight: 700;
      font-size: 26px;
      color: #5cdb95;
    }
    .content__learn-list {
      display: flex;
      flex-direction: column;
      margin-top: 20px;
      gap: 8px;
    }
    .content__learn-list-item {
      display: flex;
      align-items: center;
      gap: 8px;
    }
  }
  .content__title {
    font-weight: 700;
    font-size: 26px;
    color: #5cdb95;
    margin-top: 50px;
  }
}
.content__section-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 30px;
  background: #131313;
  border: #2e363c 1px solid;
  :nth-child(1) {
    font-weight: 700;
    font-size: 16px;
    color: #ffffff;
  }
}
.content__section-videos {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 15px 30px;
  background: #000000;
  border: #2e363c 1px solid;
  .content__section-videos-name {
    display: flex;
    align-items: center;
    gap: 15px;
    padding: 0px 20px;
    cursor: pointer;
    p {
      font-weight: 500;
      font-size: 14px;
      color: #ffffff;
      text-decoration: underline;
      color: #5cdb95;
      text-underline-offset: 5px;
      transition: all 0.3s ease;
    }
  }
  .content__section-videos-name:hover p {
    color: #ffffff;
  }
  .content__section-videos-duration {
    color: #9a9a9a;
    font-weight: 500;
    font-size: 14px;
  }
}
.buy-form {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 25px;
  .form-inputs {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
    .buy-form__num,
    .buy-form__date,
    .buy-form__cvv {
      width: 100%;
      border: none;
      border-bottom: 1px solid #ffffff;
      padding: 5px 10px;
      background: transparent;
      outline: none;
      margin: 0 auto;
      color: white;
      font-weight: 500;
      font-size: 16px;
    }
    .buy-form__date {
      width: 70%;
    }
    .buy-form__cvv {
      width: 30%;
    }
    input::placeholder {
      color: #b3b3b3;
      font-weight: 500;
      font-size: 16px;
    }
    img {
      width: 130px;
    }
    .owner {
      text-transform: uppercase;
    }
    .owner::placeholder {
      text-transform: none;
    }
  }
  .success_buy {
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 500;
    font-size: 16px;
    color: #00cb07;
  }
}
</style>
