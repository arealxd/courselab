<script setup lang="ts">
import HeaderC from '@/components/HeaderC.vue'
import FooterC from '@/components/FooterC.vue'
// import { ref } from 'vue'
// import { useRouter } from 'vue-router'
// const router = useRouter()

window.scrollTo(0, 0)
</script>

<template>
  <HeaderC />
  <div class="container">
    <div class="about">
      <p>We share knowledge with the world</p>
      <img src="/img/about.png" alt="" />
    </div>
    <div class="info">
      <p class="info__title">Improving lives through learning</p>
      <p class="info__description">
        Whether you want to learn or to share what you know, you’ve come to the right place. As a
        global destination for online learning, we connect people through knowledge.
      </p>
      <img src="/img/about_info.png" alt="" />
    </div>
  </div>
  <div class="facts">
    <div class="facts__container container">
      <p class="facts__container-title">We just keep growing</p>
      <p class="facts__container-description">
        Our global community and our course catalog get bigger every day. Check out our latest data
        for the last year.
      </p>
      <div class="facts__container-cards">
        <div class="facts__container-cards__card">
          <p class="facts__container-cards__card-title">200K+</p>
          <p class="facts__container-cards__card-description">Learners</p>
        </div>
        <div class="facts__container-cards__card">
          <p class="facts__container-cards__card-title">10K+</p>
          <p class="facts__container-cards__card-description">Teachers</p>
        </div>
        <div class="facts__container-cards__card">
          <p class="facts__container-cards__card-title">120K+</p>
          <p class="facts__container-cards__card-description">Courses</p>
        </div>
        <div class="facts__container-cards__card">
          <p class="facts__container-cards__card-title">50K+</p>
          <p class="facts__container-cards__card-description">Course enrollments</p>
        </div>
      </div>
    </div>
  </div>
  <FooterC />
</template>

<style scoped lang="scss">
.about {
  padding: 40px 60px 40px 145px;
  background: #383535;
  border-radius: 24.6857px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
  p {
    font-weight: 700;
    font-size: 50px;
    line-height: 1;
    color: #ffffff;
    max-width: 350px;
  }
  img {
    max-width: 600px;
  }
}
.info {
  display: flex;
  flex-direction: column;
  padding-top: 70px;
  padding-bottom: 120px;
  align-items: center;
  justify-content: center;
  .info__title {
    font-weight: 700;
    font-size: 45px;
    line-height: 1;
    color: #5cdb95;
    max-width: 700px;
    text-align: center;
  }
  .info__description {
    font-weight: 400;
    font-size: 20px;
    line-height: 28px;
    color: #dddddd;
    max-width: 662px;
    margin-top: 15px;
    margin-bottom: 25px;
    text-align: center;
  }
  img {
    max-width: 500px;
  }
}
.facts {
  background: rgb(119, 0, 255);
  padding: 100px 0px;
  .facts__container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .facts__container-title {
      font-weight: 700;
      font-size: 45px;
      line-height: 1;
      color: #ffffff;
      max-width: 700px;
      text-align: center;
    }
    .facts__container-description {
      font-weight: 400;
      font-size: 20px;
      line-height: 28px;
      color: #ffffff;
      max-width: 700px;
      margin-top: 15px;
      margin-bottom: 25px;
      text-align: center;
    }
    .facts__container-cards {
      display: flex;
      align-items: center;
      justify-content: space-around;
      width: 100%;
      padding: 0px 120px;
    }
    .facts__container-cards__card {
      display: flex;
      flex-direction: column;
      width: 100%;
      align-items: center;
      justify-content: center;
      .facts__container-cards__card-title {
        font-size: 35px;
        font-weight: 700;
        color: white;
      }
      .facts__container-cards__card-description {
        font-size: 18px;
        font-weight: 500;
        color: white;
      }
    }
  }
}
</style>
