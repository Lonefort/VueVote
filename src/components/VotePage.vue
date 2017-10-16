<template>
  <div class="vote">
    <ul v-if="onePerson">
      <li v-on:click='addPointToPerson'>
        <img class="photos" v-bind:src="onePerson.imgUrl" />
        <h1 class="fire">{{ onePerson.name }}</h1>
        <h1 class="burn">{{ onePerson.score }}</h1>
      </li>
      <li v-on:click='addPointToCharacter'>
        <img class="photos" v-bind:src="oneCharacter.imgUrl" />
        <h1 class="burn">{{ oneCharacter.name }}</h1>
        <h1 class="fire">{{ oneCharacter.score }}</h1>
      </li>
    </ul>
    <h1 v-else class='animate'>
    <span class="fire">S</span>
    <span class="burn">t</span>
    <span class="fire">a</span>
    <span class="burn">r</span>
    <span class="fire">t</span>
    <span class="burn">!</span>
    </h1>
    <button v-on:click="handler">
      <h1 class='animate'>
      <span class="fire">B</span>
      <span class="burn">A</span>
      <span class="fire">T</span>
      <span class="burn">T</span>
      <span class="fire">L</span>
      <span class="burn">E</span>
      <span class="fire">!</span>
      </h1>
    </button>
  </div>
</template>

<script>
export default {
  name: 'VotePage',
  data () {
    return {
      msg: 'Click to start battle!',
      persons: '',
      characters: '',
      onePerson: '',
      oneCharacter: '',
      pressed: false
    }
  },
  methods: {
    addPointToPerson () {
      if (this.pressed === false) {
        this.pressed = true
        this.persons.find(el => {
          if (el.name === this.onePerson.name) {
            el.score += 1
          }
        })
      } else {
        alert('Stop cheating!')
      }
    },
    addPointToCharacter () {
      if (this.pressed === false) {
        this.pressed = true
        this.oneCharacter.score += 1
      } else {
        alert('Stop cheating!')
      }
    },
    getPair () {
      this.pressed = false
      var getPerson = this.persons[Math.floor(Math.random() * this.persons.length)]
      var getCharacter = this.characters[Math.floor(Math.random() * this.characters.length)]
      this.onePerson = getPerson
      this.oneCharacter = getCharacter
    },
    getQuote () {
      this.$http
        .get('https://randomapi.com/api/5rjijen7?key=Q0BE-ST7X-C520-Y72G').then(data => {
          console.log(data)
          console.log(this.quote)
          this.persons = data.body.results[0].persons
          this.characters = data.body.results[0].characters
        }).then(data => this.getPair())
    },
    handler () {
      if (this.persons) {
        this.getPair()
      } else {
        this.getQuote()
        this.getPair()
      }
    }
  }
}
</script>

<style scoped>
h1 {
  background-color: black;
  -webkit-margin-before: 0em;
  -webkit-margin-after: 0em;
  -webkit-margin-start: 0px;
  -webkit-margin-end: 0px;
}
.vote {
  background-color: black;
  position: relative;
  width: 100%;
  height: 100%;
}
.photos {
  background-color: black;
  position: relative;
  border-radius: 50px;
  width: 100%;
  height: 500px;
}
ul {
  position: relative;
  top: 10%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  -webkit-margin-before: 0em;
  -webkit-margin-after: 0em;
  -webkit-margin-start: 0px;
  -webkit-margin-end: 0px;
}
span {
  color: #000;
  font-family: 'Nosifer', cursive;
  font-size: 3em;
  text-transform: lowercase;
  vertical-align: middle;
  letter-spacing: .2em;
}
button {
  position: fixed;
  bottom: 0;
  left: 33%;
  right: 33%;
  height: 15%;
  background-color: black; /* Green */
  border: none;
  border-radius: 10px;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: flex;
  justify-content: center;
  /*font-size: 16px;*/
}
.animate {
  /*background-color: rgba(256,256,256,.03);*/
  background-image: -webkit-linear-gradient(top, #111, #0c0c0c);
  background-image: -moz-linear-gradient(top, #111, #0c0c0c);
  background-image: -ms-linear-gradient(top, #111, #0c0c0c);
  background-image: -o-linear-gradient(top, #111, #0c0c0c);
  text-align: center;
  line-height: 6em;
  text-transform: uppercase;
  letter-spacing: .3em;
  white-space:nowrap;
}
.fire {
  animation: animation 1s ease-in-out infinite alternate;
  -moz-animation: animation 1s ease-in-out infinite alternate;
  -webkit-animation: animation 1s ease-in-out infinite alternate;
  -o-animation: animation 1s ease-in-out infinite alternate;
  -o-animation: animation .65s ease-in-out infinite alternate;
}
.burn{
  animation: animation .65s ease-in-out infinite alternate;
  -moz-animation: animation .65s ease-in-out infinite alternate;
  -webkit-animation: animation .65s ease-in-out infinite alternate;
}
@keyframes animation
{
0% {text-shadow: 0 0 20px #fefcc9,
  10px -10px 30px #feec85,
  -20px -20px 40px #ffae34,
  20px -40px 50px #ec760c,
  -20px -60px 60px #cd4606,
  0 -80px 70px #973716,
  10px -90px 80px #451b0e;}
100% {text-shadow: 0 0 20px #fefcc9,
  10px -10px 30px #fefcc9,
  -20px -20px 40px #feec85,
  22px -42px 60px #ffae34,
  -22px -58px 50px #ec760c,
  0 -82px 80px #cd4606,
  10px -90px 80px  #973716;}
}
@-webkit-keyframes animation
{
0% {text-shadow: 0 0 20px #fefcc9,
  10px -10px 30px #feec85,
  -20px -20px 40px #ffae34,
  20px -40px 50px #ec760c,
  -20px -60px 60px #cd4606,
  0 -80px 70px #973716,
  10px -90px 80px #451b0e;}
100% {text-shadow: 0 0 20px #fefcc9,
  10px -10px 30px #fefcc9,
  -20px -20px 40px #feec85,
  22px -42px 60px #ffae34,
  -22px -58px 50px #ec760c,
  0 -82px 80px #cd4606,
  10px -90px 80px  #973716;}
}
li {
  width: 30%;
  height: 100%;
  position: relative;
  margin: 10px;
  display: flex;
  padding: 10px;
  flex-direction: column;
}
</style>
