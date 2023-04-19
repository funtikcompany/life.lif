
<template>
  <div class="test bg">
    <img v-if="!status" class="test-img-left" src="../assets/img/lightning-left.svg" alt="">
    <img v-if="!status" class="test-img-rigth" src="../assets/img/lightning-rigth.svg" alt="">
    <div class="container">
      <Range v-if="status" :progress="progressPercentage" :maxProgress="questions.length"></Range>
      <div v-if="currentQuestion">
        <question :id="currentQuestion.id" :img="currentQuestion.img" :question="currentQuestion.question"
          :answers="currentQuestion.answers" :typeBtn="currentQuestion.typeBtn" @answer-selected="saveAnswer"></question>
      </div>
      <div v-else class="finish">
        <div v-if="status" class="finish-before">
          <h2 class="finish-title">Oбработка результатов</h2>
          <div class="finish-animation"></div>
          <p>Определение стиля мышления..................................................................</p>
        </div>
        <div v-else class="finish-after">
          <h3 class="finish-after-title">
            Ваш результат рассчитан:
          </h3>
          <p class="finish-after-type"><a href="">Вы относитесь к 3%</a> респондентов, чей уровень интеллекта более чем на
            15 пунктов отличается от среднего в большую или меньшую сторону! </p>
          <h3 class="finish-after-subtitle">Скорее получите свой результат!
          </h3>
          <p class="finish-after-security">В целях защиты персональных
            данных результат теста, их подробная интерпретация и рекомендации доступны в виде голосового сообщения по
            звонку с вашего мобильного телефона
          </p>
          <p class="finish-after-record">Звоните скорее, запись доступна всего </p>
          <div>
            <Timer></Timer>
          </div>

          <button @click="fetchData" class="btn-call"><img src="../assets/img/call-btn.svg" alt=""> Позвонить и прослушать
            результат </button>

          <div>
            <div v-if="loader" class="loader"></div>
            <div v-if="tableVisible">
              <Table :data="getDate"></Table>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="container">
        <p class="footer-copy">TERMENI SI CONDITII: ACESTA ESTE UN SERVICIU DE DIVERTISMENT. PRIN FOLOSIREA LUI DECLARATI
          CA
          AVETI 18 ANI IMPLINITI, </p>
      </div>
    </div>
  </div>
</template>

<script>
import Question from '@/components/Question.vue';
import Range from '@/components/Range.vue';
import Timer from '@/components/Timer.vue'
import Table from '@/components/Table.vue'
import axios from 'axios'

export default {
  components: {
    Question,
    Range,
    Timer,
    Table
  },
  data() {
    return {
      currentQuestionIndex: 0,
      answers: [],
      questions: [
        {
          question: 'Ваш пол:',
          answers: ['мужчина', 'женщина'],
          id: 1,
          typeBtn: 'input',
        },
        {
          question: 'Укажите ваш возраст: ',
          answers: ['До 18', 'От 18 до 28', 'от 29 до 35', 'От 36'],
          id: 2,
          typeBtn: 'input',
        },
        {
          question: 'Выберите лишнее:',
          answers: ['Дом', 'Шалаш', 'Бунгало', 'Скамейка', 'Хижина'],
          id: 3,
          typeBtn: 'input',
        },
        {
          question: 'Продолжите числовой ряд: 18  20  24  32',
          answers: ['62', '48', '74', '57', '60', '77'],
          id: 4,
          typeBtn: 'input',
        },
        {
          question: 'Выберите цвет, который сейчас наиболее Вам приятен:',
          answers: ['#A8A8A8', '#0000A9', '#00A701', '#F60100', '#FDFF19', '#A95403', '#000000', '#850068', '#46B2AC'],
          id: 5,
          typeBtn: 'colorBox'
        }
        ,
        {
          question: 'Отдохните пару секунд, еще раз Выберите цвет, который сейчас наиболее Вам приятен:',
          answers: ['#00A701', '#A8A8A8', '#850068', '#0000A9', '#A95403', '#FDFF19', '#000000', '#F60100', '#46B2AC'],
          id: 6,
          typeBtn: 'colorBox'
        }
        ,
        {
          question: 'Какой из городов лишний?',
          answers: ['Вашингтон', 'Лондон', 'Париж', 'Нью-Йорк', 'Москва', 'Оттава'],
          id: 7,
          typeBtn: 'input'
        },
        {
          question: 'Выберите правильную фигуру из четырёх пронумерованных.',
          answers: ['1', '2', '3', '4'],
          id: 8,
          typeBtn: 'btn',
          img: 'image1.png',
        },
        {
          question: 'Вам привычнее и важнее:',
          answers: ['Наслаждаться каждой минутой проведенного времени', 'Быть устремленными мыслями в будущее', 'Учитывать в ежедневной практике прошлый опыт'],
          id: 9,
          typeBtn: 'input'
        },
        {
          question: 'Какое определение, по-Вашему, больше подходит к этому геометрическому изображению: ',
          answers: ['оно остроконечное', 'оно устойчиво', 'оно-находится в состоянии равновесия'],
          id: 10,
          typeBtn: 'input',
          img: 'image2.png',
        },
        {
          question: 'Вставьте подходящее число',
          answers: ['34', '36', '53', '44', '66', '42'],
          id: 11,
          typeBtn: 'btn',
          img: 'image3.png',
        },
      ],
      status: true,
      tableVisible: false,
      loader: false,
      getDate: '',
      show: false
    };
  },
  computed: {
    totalQuestions() {
      return this.questions.length;
    },
    currentQuestion() {
      if (!this.questions[this.currentQuestionIndex]) {
        setTimeout(() => {
          this.status = false
        }, 5000)
      }
      return this.questions[this.currentQuestionIndex];
    },
    progressPercentage() {
      return ((this.currentQuestionIndex + 1) / this.totalQuestions) * (this.totalQuestions - .5);
    },
  },
  methods: {
    saveAnswer(answer) {
      this.answers.push(answer);
      this.currentQuestionIndex++;
    },
    fetchData() {

      axios.get("https://swapi.dev/api/people/1/")
        .then(response => {
          this.getDate = response.data;
          this.loader = true;
          setTimeout(() => {
            this.tableVisible = true;
            this.loader = false;
          }, 1000)
        })
        .catch(error => {
          console.log(error);
        });
    },
  },
};


</script>

