<template>
  <Header></Header>
  <router-view />
</template>

<script>
import Header from '@/components/Header.vue';
export default {
  components: {
    Header: Header
  }, data() {
    return {
      show: false
    };
  }
}
</script>
