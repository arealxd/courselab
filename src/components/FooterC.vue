<script setup lang="ts">
import { useRouter } from 'vue-router'
const router = useRouter()
</script>

<template>
  <div class="full-footer-bg">
    <div class="container">
      <div class="footer">
        <div class="footer__blocks">
          <div class="footer__list">
            <p @click="router.push('/courses')">All courses</p>
            <p @click="router.push('/about')">About us</p>
            <p @click="router.push('/auth')">Log in</p>
          </div>
          <div class="footer__list contact">
            <a href="tel:+77055254909"><span>Contact phone:</span> +7 (705) 525-49-09</a>
            <a href="mailto:course.lab@gmail.com"><span>E-mail:</span> course.lab@gmail.com</a>
            <a href="https://2gis.kz/almaty/geo/70030076160263029" target="_blank"
              ><span>Address:</span> Kazakhstan, Almaty, Abaya 90</a
            >
          </div>
        </div>
        <div class="footer__copyright">
          <img class="footer__copyright-logo" src="/img/logo.png" alt="" />
          <p class="footer__copyright-copyright">© 2023 CourseLab, Inc.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.full-footer-bg {
  background: #a43227;
  width: 100%;
}
.footer {
  padding: 28px 48px 32px 48px;
  background: #a43227;
}
.footer__blocks {
  display: flex;
  gap: 150px;
}
.footer__list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  p,
  a {
    font-weight: 400;
    font-size: 13px;
    color: #ffffff;
    cursor: pointer;
    max-width: 150px;
    transition: all 0.3s ease;
  }
  p:hover,
  a:hover {
    color: #5cdb95;
    text-decoration: underline;
    text-underline-offset: 5px;
  }
}
.contact {
  p,
  a {
    white-space: nowrap;
  }
  span {
    font-weight: 700;
  }
}
.footer__copyright {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 75px;
  .footer__copyright-copyright {
    color: #ffffff;
    font-weight: 400;
    font-size: 12px;
  }
}
</style>
