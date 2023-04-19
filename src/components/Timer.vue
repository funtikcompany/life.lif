<template>
  <div v-if="timeLeft > 0">
    <div class="timer"> <span>{{ minutes }}:{{ seconds }}</span> Минут</div>
  </div>
  <div v-else>
    <h2 class="timer-end">Час вийшов!</h2>
  </div>
</template>

<script>
export default {
  data() {
    return {
      deadline: new Date().getTime() + 10 * 60 * 1000, // 10 хвилин в мілісекундах
      timeLeft: 0,
    };
  },
  created() {
    setInterval(this.updateTimer, 1000);
  },
  methods: {
    updateTimer() {
      const now = new Date().getTime();
      this.timeLeft = this.deadline - now;

      if (this.timeLeft <= 0) {
        clearInterval();
      }
    },
  },
  computed: {
    minutes() {
      return Math.floor(this.timeLeft / (60 * 1000));
    },
    seconds() {
      return Math.floor((this.timeLeft % (60 * 1000)) / 1000);
    },
  },
};
</script>


