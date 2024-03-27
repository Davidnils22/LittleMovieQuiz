<template>
  <div class="matte-quiz">
    <h1>Film Quiz</h1>
    <div v-if="!quizOver && quizStarted" class="question-container">
    <input class="range" type="range" min="0" :max="questions.length - 1" v-model="currentQuestionIndex" @mousedown.prevent :class="{ 'green': currentQuestionIndex === questions.length - 1 }" >
      <h2>Fråga {{ currentQuestionIndex + 1 }}</h2>
      <p class="question">{{ currentQuestion.question }}</p>
      <div class="options-container">
        <button v-for="(option, index) in currentQuestion.options" :key="index" @click="checkAnswer(option)" class="option-button">{{ option }}</button>
      </div>
    </div>

    <div v-else-if="quizStarted" class="result-container">
      <h2>Quizet är slut!</h2>
      <p>Du fick {{ score }} av {{ questions.length }} frågor rätt.</p>
      <h3> {{ calculatePercantage() }} % </h3>

      <p v-if="calculatePercantage() < 50">Bättre kan du!</p>
      <p v-else>Snyggt jobbat!</p>

      <div class="button-container">
      <input class="button" type="button" value="Starta om" @click="restartQuiz">
      <input class="button"type="button" value="Nytt Quiz">
      </div>

    </div>
    <input class="button" type="button" value="Starta" @click="startQuiz" v-show="!quizStarted">
  </div>

  

</template>

<script>
export default {
  data() {  
    return {    // Skapar array med objekt, innerhållandes frågor, val & rätt svar.
      questions: [
        {
          question: "Vilken film vann 'Bästa film' vid Oscarsgalan 2020? " ,
          options: [" Joker", " Parasite", " 1917", " Once Upon a Time in Hollywood "],
          correctAnswer: "Parasite"
        },
        {
          question: "Vem regisserade filmen 'Inception' från 2010?",
          options: ["Christopher Nolan", "Steven Spielberg", "Quientin Tarantino", "Martin Scorsese"],
          correctAnswer: "Christopher Nolan"
        },
        {
          question: "Vilken skådespelare spelade huvudrollen i filmen 'The Shawshank Redemption' ",
          options:  ["Tom Hanks", "Tim Robbins", "Morgan Freeman", "Brad Pitt"],
          correctAnswer: "Tim Robbins"
        },
        {
          question: "Vad är namnet på den första filmen i 'The Lord of the Rings'-trilogin?",
          options: ["The Two Towers", "The Return of the King", "The Fellowship of the Ring", "The Hobbit"],
          correctAnswer: "The Fellowship of the Ring"
        },
        {
          question: "I vilken film spelar Leonardo DiCaprio karaktären Jordan Belfort, en mäklare på Wall Street?",
          options: ["The Wolf of Wall Street", "Shutter Island", "Catch Me If You Can", "Blood Diamond"],
          correctAnswer: "The Wolf of Wall Street"
        },
        {
          question: "Vilken animerad film handlar om en ung fisk vid namn Nemo som tas tillfånga av en dykare och hamnar i ett akvarium?",
          options: ["Finding Nemo", "Shark Tale", "Finding Dory", "The Little Mermaid"],
          correctAnswer: "Finding Nemo"
        },
        {
          question: "Vilken skådespelare som ursprungligen skulle spela rollen som Professor Severus Snape tackade nej, vilket ledde till att rollen istället gick till Alan Rickman?",
          options: ["Jeremy Irons", "Tim Roth", "Ian McKellen", "Ralph Fiennes"],
          correctAnswer: "Tim Roth"
        },
        {
          question: "Vart utspelar sig filmen Dune?",
          options: ["Planeten Arrakis", "Månen Endor", "Stjärnsystemet Alpha Centauri", "Galaxen Andromeda"],
          correctAnswer: "Planeten Arrakis"
        }
      ],
      currentQuestionIndex: 0,  
      score: null,
      quizOver: false,
      quizStarted: false,
      waitingForResult: false
    };
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex];
    }
  },
  methods: {
    // Startar spelet!
    startQuiz() {
      console.log('Quiz startar...')
      this.quizStarted = true;
      this.score = 0;
      this.shuffle();
    },
    // Kontrollerar svar!
    checkAnswer(selectedOption) {
    console.log('Svar kontrolleras...');
    if (selectedOption === this.currentQuestion.correctAnswer) {
    this.score++;

  } // Kommer till nästa fråga!
  if (this.currentQuestionIndex < this.questions.length - 1) {
    console.log('Nästa fråga...');
    this.currentQuestionIndex++;

  } else { // Nu är spelet slut!
    console.log('Quizet är slut...');
    this.waitingForResult = true;
    console.log('Väntar på resultatet..', this.waitingForResult)
    this.resultTimeout = setTimeout(() => {
      this.waitingForResult = false;
      this.quizOver = true;
      this.saveScore();
    }, 1500);
  }
},

  shuffle() {
  // Randomisera frågorna
  console.log('Blandar frågorna & svarsalternativen...')
  this.questions = this.shuffleArray(this.questions);

  // Randomisera svarsalternativen för varje fråga
  this.questions.forEach(question => {
    question.options = this.shuffleArray(question.options);
  });
}, // Här blandar jag arrayen.
  shuffleArray(array) {
  for (let i = array.length - 1; i > 0; i--) {
    console.log('Blandar arrayen')
    const randomIndex = Math.floor(Math.random() * (i + 1));
    // Byt plats på elementen array[i] och array[randomIndex]
    [array[i], array[randomIndex]] = [array[randomIndex], array[i]];
  }
  return array;
},
    // Sparar så endast det högsta resultatet i localStorage.
    saveScore() {
      console.log('Sparar poängen...')
    if (this.quizOver) {
      const highScore = localStorage.getItem('highScore');
      if (!highScore || this.score > parseInt(highScore)) {
      localStorage.setItem('highScore', this.score.toString());
    }
  }
},  // Skapar en knapp där man kan starta om spelet.
restartQuiz() {
  console.log('Quizet startar om...');
  // Rensa timeout om det finns
  if (this.resultTimeout) {
    clearTimeout(this.resultTimeout);
  }
  this.quizStarted = true;
  this.quizOver = false;
  this.currentQuestionIndex = 0;
  this.score = null;
  this.shuffle();
},
  // Räknar ut % på antal rätt.
  
calculatePercantage(){
  if(this.score === null) return 0;
  return ((this.score / this.questions.length) * 100)
}
  }
};
</script>

<style scoped>
.matte-quiz {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  border: 2px solid #007bff; 
  background-color: rgba(118, 7, 128, 0.5);
  border-radius: 10px; 
  padding: 20px; 
  margin: 10px;
  height: 400px;
  width: 700px; 
  overflow: auto; 
}

.question-container {
  margin-bottom: 20px;
}
h1, h2{
  color: white;
  font-size: 1.8rem;
}
h3{
  font-size: 2rem;
}
p{
  font-size: 1.9rem;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  color: white;
}
.question {
  font-family: 'Courier New', Courier, monospace;
  font-size: 1.7rem;
  margin-bottom: 10px;
  color: white;
  
}

.options-container {
  display: flex;
  justify-content: space-between; 
}

.option-button {
  width: 150px; 
  margin: 15px;
  padding: 10px;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  background-color: #4b154d;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

.option-button:hover {
  background-color: #0056b3;
}

.result-container {
  margin-top: 20px;

}
.button {
  cursor: pointer;
  position: relative;
  padding: 10px 24px;
  font-size: 18px;
  color: rgb(186, 181, 168);
  border: 2px solid rgb(48, 65, 141);
  border-radius: 34px;
  background-color: transparent;
  font-weight: 600;
  transition: all 0.3s cubic-bezier(0.23, 1, 0.320, 1);
  overflow: hidden;
  margin-top: 50px;
  margin-right: 10px;
}
.button-container{
  display: inline-block;
  margin: 25px;
}

.button::before {
  content: '';
  position: absolute;
  inset: 0;
  margin: auto;
  width: 50px;
  height: 50px;
  border-radius: inherit;
  scale: 0;
  z-index: -1;
  background-color: rgb(193, 163, 98);
  transition: all 0.6s cubic-bezier(0.23, 1, 0.320, 1);
}

.button:hover::before {
  scale: 3;
}

.button:hover {
  color: #212121;
  scale: 1.1;
  box-shadow: 0 0px 20px rgba(193, 163, 98,0.4);
}

.button:active {
  scale: 1;
}
.range {
  width: 100%;
  height: 10px;
  
  background: linear-gradient(to right, #f4a261, #2a9d8f); /* Bakgrundsfärg med gradient */
  border-radius: 5px; /* Rundade kanter */
}

.range::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  background: #f4a261; /* Tumme färg */
  border-radius: 50%; /* Rundad tumme */
  cursor: pointer;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.5); /* Ljus skugga */
}

.range::-moz-range-thumb {
  width: 20px;
  height: 20px;
  background: #f4a261;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.5);
}

.range.green {
  background: linear-gradient(to right, #58b368, #106113); /* Grön gradient för rätt svar */
}

.range.green::-webkit-slider-thumb {
  background: #58b368; /* Grön tumme färg för rätt svar */
}

.range.green::-moz-range-thumb {
  background: #58b368;
}
</style>