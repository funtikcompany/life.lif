<template>
  <div>
    <section class="intro bg">
      <div class="container">
        <p class="intro-suptitle">
          Пройдите точный и быстрый
        </p>
        <h1 class="intro-title">
          тест на определение IQ
        </h1>
        <img class="intro-img" src="../assets/img/intro/rain_bk3.png" alt="">
        <router-link class="intro-btn-test" to="/test">Пройти тест</router-link>
        <p class="intro-subtitle"><span> и получите рекомендации
            по развитию своего интеллекта</span>
          и улучшению финансового благосостояния и личной жизни</p>
        <button class="intro-btn"><img src="../assets/img/intro/arrow-top.svg" alt=""> подробнее</button>
      </div>
    </section>
    <div class="professional">
      <div class="container">
        <p class="professional-info"> <img src="@/assets/img/professional/left.svg" alt=""> Профессиональный IQ-тест
          позволяет не только определить коэффициент
          вашего
          интеллекта,
          но и выработать список рекомендаций для повышения этого показателя. <img
            src="@/assets/img/professional/right.svg" alt=""></p>
      </div>
    </div>
    <div class="about">
      <div class="container">
        <p class="about-info">Также по результатам теста
          <span> вы получите</span>
          подробные <span>советы</span> по определению наиболее перспективной <span>для вашего типа</span> интеллекта
          <span> сферы
            деятельности,</span>
          которая принесет вам скорейший финансовый результат.
        </p>
        <div class="about-rigth">
          <img class="about-img" src="../assets/img/about/aboutimg.png" alt="">
          <router-link class="intro-btn-test" to="/test">Пройти тест</router-link>
        </div>
      </div>
    </div>

    <footer class="footer bg">
      <img class="footer-img-left" src="../assets/img/lightning-left.svg" alt="">
      <img class="footer-img-rigth" src="../assets/img/lightning-rigth.svg" alt="">
      <div class="container">
        <p class="footer-suptitile">Прохождение теста займет у вас не более <span>12 минут</span>, а его результаты вы
          сможете
          <span>использовать всю жизнь.</span>
        </p>
        <p class=footer-info>Профессиональная интерпретация и детально проработанные рекомендации позволят вам качественно
          изменить все
          аспекты своей жизни: от финансового до любовного.</p>
        <router-link class="footer-btn-test" to="/test">Пройти тест</router-link>
        <p class="footer-copy"> <img src="../assets/img/img.png" alt=""> 2019</p>
      </div>
    </footer>
  </div>
</template>

<script>

export default {
}
</script>
