<script setup lang="ts">
import HeaderC from '@/components/HeaderC.vue'
import FooterC from '@/components/FooterC.vue'
import coursesJson from '@/json/courses.json'
import { ref } from 'vue'
import { useRouter } from 'vue-router'
const router = useRouter()

const allCourses = ref(coursesJson)

const applyFilter = () => {
  console.log('filter')
  window.scrollTo(0, 0)
}

window.scrollTo(0, 0)
</script>

<template>
  <HeaderC />
  <div class="container">
    <div class="courses">
      <p>Courses</p>
      <div class="courses__content">
        <div class="courses__filter">
          <div class="courses__filter-title">
            <svg
              width="20"
              height="21"
              viewBox="0 0 20 21"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M9 15.2031H13V13.2031H9V15.2031ZM2 3.20312V5.20312H20V3.20312H2ZM5 10.2031H17V8.20312H5V10.2031Z"
                fill="#E0E1E3"
              />
            </svg>

            <p>Filter</p>
          </div>
          <hr />
          <form @submit.prevent="applyFilter">
            <select class="courses__filter-sort">
              <option selected hidden>Sort by</option>
              <option value="popular">Popularity</option>
              <option value="desc">Descending price</option>
              <option value="asc">Ascending price</option>
            </select>
            <select class="courses__filter-sort">
              <option selected hidden>Topic</option>
              <option value="en">JavaScript</option>
              <option value="ru">PHP</option>
              <option value="kz">Laravel</option>
              <option value="kz">Flutter</option>
              <option value="kz">Java</option>
              <option value="kz">Python</option>
              <option value="kz">Node.Js</option>
              <option value="kz">С++</option>
              <option value="kz">Golang</option>
              <option value="kz">UX/UI Design</option>
              <option value="kz">Mathematics</option>
              <option value="kz">Physics</option>
            </select>
            <select class="courses__filter-sort">
              <option selected hidden>Rating</option>
              <option value="4.5+">4.5+</option>
              <option value="4.0+">4.0+</option>
              <option value="3.0+">3.0+</option>
            </select>
            <select class="courses__filter-sort">
              <option selected hidden>Video Duration</option>
              <option value="0-10">0-10 hours</option>
              <option value="10-20">10-20 hours</option>
              <option value="20-30">20-30 hours</option>
              <option value="30+">30+ hours</option>
            </select>
            <select class="courses__filter-sort">
              <option selected hidden>Price</option>
              <option value="paid">Paid</option>
              <option value="free">Free</option>
            </select>
            <select class="courses__filter-sort">
              <option selected hidden>Language</option>
              <option value="en">English</option>
              <option value="ru">Руский</option>
              <option value="kz">Қазақша</option>
            </select>
            <button class="courses__filter-apply">Apply</button>
          </form>
        </div>
        <div class="courses__list">
          <div
            class="courses__list-course"
            v-for="i in allCourses"
            :key="i.id"
            @click="router.push('/details/' + i.id + '/' + 2)"
          >
            <img :src="i.image" alt="" />
            <div class="course__info">
              <div class="course__info-title">
                <p class="course__info-name">{{ i.title }}</p>
                <p class="course__info-price">{{ i.price }} $</p>
              </div>
              <p class="course__info-description">{{ i.description }}</p>
              <p class="course__info-author">{{ i.author }}</p>
              <div class="course__info-rating">
                <img src="/img/star.png" alt="" />
                <p>{{ i.rating }}</p>
              </div>
              <div class="course__info-hours">
                <p>{{ i.totalHours }} total hours</p>
                <svg
                  width="6"
                  height="6"
                  viewBox="0 0 6 6"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M3.13513 5.42275C4.45513 5.42275 5.51113 4.36675 5.51113 3.04675C5.51113 1.72675 4.45513 0.67075 3.13513 0.67075C1.81513 0.67075 0.759125 1.72675 0.759125 3.04675C0.759125 4.36675 1.81513 5.42275 3.13513 5.42275Z"
                    fill="#6A6F73"
                  />
                </svg>
                <p>{{ i.lecturesQuantity }} lectures</p>
              </div>
            </div>
          </div>
        </div>
        <div class="courses__ad">
          <a href="https://www.google.com/" target="_blank">
            <img src="/img/ad.png" alt="" />
          </a>
        </div>
      </div>
    </div>
  </div>
  <FooterC />
</template>

<style scoped lang="scss">
form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
hr {
  border: 1px solid #5c846f;
  margin: 5px 0px;
}
.courses__content {
  display: flex;
  margin-top: 40px;
  gap: 40px;
}
.courses__filter {
  display: flex;
  flex-direction: column;
  gap: 20px;
  .courses__filter-title {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    padding: 10px 0px;
    border: 1px solid #5cdb95;
    width: 100%;
    p {
      font-weight: 700;
      font-size: 20px;
      color: #e0e1e3;
    }
  }
  .courses__filter-sort {
    padding: 10px 15px;
    border: 1px solid #ffffff;
    width: 100%;
    background: #1a1a1a;
    color: #e0e1e3;
    font-weight: 500;
    font-size: 14px;
    outline: none;
    border-radius: 10px;
    option {
      background: #2c1b56;
      color: #e0e1e3;
      font-weight: 500;
      font-size: 14px;
    }
  }
  .courses__filter-apply {
    padding: 10px 20px;
    border: 1px solid #5cdb95;
    width: 100%;
    background: #1a1a1a;
    color: #5cdb95;
    font-weight: 600;
    font-size: 14px;
    outline: none;
    border-radius: 10px;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  .courses__filter-apply:hover {
    background: #5cdb95;
    color: #1a1a1a;
  }
}
.courses {
  padding: 20px 0px 20px 150px;
  padding-bottom: 100px;
  display: flex;
  flex-direction: column;
  p {
    font-weight: 700;
    font-size: 40px;
    color: #ffffff;
  }
}
.courses__list {
  display: flex;
  flex-direction: column;
  gap: 30px;

  .courses__list-course {
    cursor: pointer;
    display: flex;
    gap: 15px;
    img {
      width: 260px;
      height: 170px;
      border-radius: 20px;
    }
    .course__info {
      display: flex;
      flex-direction: column;
      gap: 5px;
      .course__info-title {
        display: flex;
        align-items: center;
        justify-content: space-between;
      }
      .course__info-name {
        font-weight: 700;
        font-size: 20px;
        color: #ffffff;
      }
      .course__info-description {
        font-weight: 400;
        font-size: 16px;
        color: #ffffff;
        max-width: 650px;
      }
      .course__info-author {
        font-weight: 400;
        font-size: 12px;
        color: #6a6f73;
      }
      .course__info-rating {
        display: flex;
        align-items: center;
        gap: 8px;
        img {
          width: 15px;
          height: 15px;
        }
        p {
          font-weight: 700;
          font-size: 14px;
          color: #ffb800;
        }
      }
      .course__info-hours {
        display: flex;
        align-items: center;
        gap: 5px;
        p {
          font-weight: 400;
          font-size: 12px;
          color: #6a6f73;
        }
      }
      .course__info-price {
        font-weight: 700;
        font-size: 18px;
        color: #5cdb95;
      }
    }
  }
}
.courses__ad {
  margin-left: auto;
  margin-right: 10px;
}
</style>
