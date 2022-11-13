<template>
  <h1>Summon the Sorting Hat!</h1>
    <div class="grid">
      <img class="candlesa" src="https://media2.giphy.com/media/TLJeQLdDIjvSxvjVyO/giphy.gif?cid=ecf05e47de3a5uxeguh3gjmdkacli3zcggyl9g861vcwla16&rid=giphy.gif&ct=s" alt="floating candles">
      <img src="@/assets/images/sortinghat.png" alt="student being sorted"/>
      <img class="candlesb" src="https://media2.giphy.com/media/TLJeQLdDIjvSxvjVyO/giphy.gif?cid=ecf05e47de3a5uxeguh3gjmdkacli3zcggyl9g861vcwla16&rid=giphy.gif&ct=s" alt="floating candles">
    </div>
  <form v-if="quizActive">
    <fieldset v-for="(question, qdex) in quizQuestions" v-bind:key="qdex">
      <h2>{{ question.text }}</h2>
      <div v-for="(house, h, hdex) in houses" v-bind:key="hdex">
        <input type="radio" :name="question.topic" :value="h" :id="h" v-model="answers[qdex]"/>
        <label :for="h">{{ house[question.topic] }}</label>
      </div>
    </fieldset>
    <button class="animate__animated animate__pulse animate__slow 5s animate__infinite" @click="gradeQuiz">Computo Resultum</button>
  </form>
  <div v-else>
    <p>Your score... {{ score }}</p>
    <!-- <p>You belong to... {{ multiply(score) }}</p>
    <p>New score? {{ newScore(score) }}</p> -->
    <p> Yer a ... {{ yourHouse(score) }}</p>
    <button id="newattempt" class="animate__animated animate__bounce animate__delay-2s" @click="restart">Try Again?</button>
  </div>
</template>

<script>

export default {
    name: 'DisplayQuiz',
    props: ['houses'],
    score: 0,
    data() {
      return {
        score: 0,
        quizActive: true,
        // baseMultiplier: 10,
        // num: 1,
        quizQuestions: [
          {
            topic: 'animal',
            text: "Which is your favorite animal?",
            godric: 'gryffindor',
            rowena: 'ravenclaw',
            helga: 'hufflepuff',
            salazar: 'slytherin'
          },
          {
            topic: 'houseColours',
            text: "Which are your favorite colors?",
            godric: 'gryffindor',
            rowena: 'ravenclaw',
            helga: 'hufflepuff',
            salazar: 'slytherin'
          },
          {
            topic: 'ghost',
            text: "Which is your favorite ghost?",
            godric: 'gryffindor',
            rowena: 'ravenclaw',
            helga: 'hufflepuff',
            salazar: 'slytherin'
          },
          {
            topic: 'element',
            text: "Which is your favorite element?",
            godric: 'gryffindor',
            rowena: 'ravenclaw',
            helga: 'hufflepuff',
            salazar: 'slytherin'
          },
        ],
        answers: Array(4),
      }

    },
    methods: {
      gradeQuiz() {
        for (const i in this.answers) {
          if (this.answers[i] == this.quizQuestions[i].godric) {
            this.score++;
          } else if
            (this.answers[i] == this.quizQuestions[i].rowena) 
            this.score+=3;
          else if (this.answers[i] == this.quizQuestions[i].helga) {
            this.score+=5;
          } else { this.score+=7;}
        }
          this.quizActive = !this.quizActive;
      }, 
      // multiply(gradeQuiz) {
      //   return gradeQuiz * this.baseMultiplier
      // },
      // newScore(gradeQuiz) {
      //   return gradeQuiz - this.num
      // },
      yourHouse(gradeQuiz) {
        if (gradeQuiz <= 9) {
          return "GGGRRRYYYFFFIINNNDOOORRRR"
        } else if (gradeQuiz >=10 || gradeQuiz <= 15) {
          return "RRRAAAVENCCLLLLAAAAWWW!"
        } else if (gradeQuiz >=16 || gradeQuiz <=22) {
          return "HHHHUUUUFFFLEPUUUUFFFF"
        }else {
          return "SSSLLLYYYYTHERRRIIINNNN"
        }
      },
       restart() {
        this.answers = Array(4);
        this.score = 0;
        this.quizActive = !this.quizActive;
      },
    }
  }

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Averia+Libre&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto+Flex:opsz,wght@8..144,200;8..144,500&display=swap');

h1 {
  font-family: Averia Libre, cursive;
}
.grid{
  display: grid;
  width: 600px;
  height: 240px;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: repeat(3, 1fr);
  margin: auto;
}
img {
  max-width: 210px;
  max-height: 240px;
  grid-area: 1 / 3 / span 1 / span 2;
}
.candlesa{
  max-width: 125px;
  grid-area: 1 / 2 / span 1 / span 1;
  z-index: 1;
}
.candlesb{
  max-width: 125px;
  grid-area: 1 / 5 / span 1 / span 1;
  z-index: 1;
}
fieldset {
  max-width: 500px;
  margin: 10px auto;
}
h2 {
  font-family: Averia Libre, cursive;
  font-size: 24px;
}
h3 {
  margin: 40px 0 0;
}
div input[type="radio"] {
  margin: 0 1em;
}
div label {
  font-family: 'Roboto Flex', sans-serif;
  display: inline-block;
  min-width: 160px;
  text-align: left;
  padding: 5px;
}
input[type=radio] {
  accent-color: #d6ad3c;
}
button {
  font-family: Averia Libre, cursive;
  font-size: 24px;
  width: 250px;
  padding: 19px 0;
  margin: 40px 2px;
  color: #FFF;
  background-color: #808080;
  border-radius: 15px;
  box-shadow: #808080;
  border: 1px solid white;
}
button:hover {
  background-color: #d6ad3c;
}
p {
  font-family: Averia Libre, cursive;
  font-size: 24px;
  margin-top: 20px;
}
#newattempt {
  font-family: Averia Libre, cursive;
  font-size: 18px;
  width: 125px;
  padding: 10px 5px;
  margin: 5px 2px;
  color: #FFF;
  background-color: #808080;
  border-radius: 15px;
  box-shadow: #808080;
  border: 1px solid white;
} 
#newattempt:hover {
  background-color: #417f3c;
}
</style>
