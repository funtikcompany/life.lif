<template>
  <nav class="nav">
    <span @click="openMenu" class="toggle"><img src="../assets/img/menu.svg" alt=""></span>
    <ul class="nav-list" :class="{ 'active': active }">
      <span @click="closedMenu" class="close"> <img src="../assets/img/close.svg" alt=""></span>
      <li class="nav-item"><router-link to="/">Главная</router-link></li>
      <li class="nav-item"><router-link to="/#info">Информация о тесте</router-link></li>
      <li class="nav-item"><router-link to="test">Пройти тест</router-link></li>
    </ul>
    <div v-if="$route.name === 'test'" class="nav-title"><img src="../assets/img/intro/rain_bk3.png" alt="">
      <span>тест на
        определение IQ</span>
    </div>
  </nav>
</template>
<script>
export default {
  name: 'header',
  data() {
    return {
      active: false,
    }
  },
  methods: {
    openMenu() {
      this.active = true
    },
    closedMenu() {
      this.active = false
    },
  },
}
</script>