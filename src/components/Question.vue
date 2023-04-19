<template>
  <div class="wrapper">
    <h2 class="question-name">{{ question }}</h2>
    <img class="question-img" v-if="img" :src="require(`@/assets/img/${img}`)" alt="">
    <ul v-if="typeBtn == 'input'">
      <li class="question" :class="{ 'selected': selectedAnswer === answer }" v-for="(answer, index) in answers"
        :key="index">
        <label class="question-info">
          <input class="input" type="radio" :name="`question-${id}`" :value="answer" v-model="selectedAnswer">
          <span>{{ answer }}</span>
        </label>
      </li>
    </ul>
    <div class="colorBox box-btn" v-else-if="typeBtn == 'colorBox'">
      <label :class="{ 'selected': selectedAnswer === answer }" v-for="(answer, index) in answers" :key="index"
        :style="{ backgroundColor: answer }" class="question-color-box">
        <input class="input" type="radio" :name="`question-${id}`" :value="answer" v-model="selectedAnswer">
      </label>
    </div>

    <div class="colorBox box-btn" v-else-if="typeBtn == 'btn'">
      <label :class="{ 'selected': selectedAnswer === answer }" v-for="(answer, index) in answers" :key="index"
        class="question-btn">
        <input class="input" type="radio" :name="`question-${id}`" :value="answer" v-model="selectedAnswer">
        <span>{{ answer }}</span>
      </label>
    </div>
    <button class="btn-next" :disabled="isNextDisabled" @click="nextQuestion()">далее</button>
  </div>
</template>

<script>
export default {
  props: {
    id: Number,
    question: String,
    answers: Array,
    img: String,
    typeBtn: String,
    correctAnswer: {
      type: String,
      required: true
    },
  },
  data() {
    return {
      selectedAnswer: null,
    };
  },
  computed: {
    isNextDisabled() {
      return !this.selectedAnswer
    }
  },
  methods: {
    nextQuestion() {
      this.$emit('answer-selected', this.selectedAnswer);
      this.selectedAnswer = null;
    }
  }
};
</script>
