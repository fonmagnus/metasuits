<template>
<div>
  <div class="md-3" v-for="card in cards">
    <!-- <h1>Test</h1> -->
    <flipper
      class="Card"
      width="270px"
      height="300px"
      :flipped="card.isFlipped"
      @click="flipCard(card)"
      
    >
      <div class="Card__face" slot="front">
        <span v-if="card.suit === '♠' || card.suit === '♣'" class="Card__value Card__value--top">{{card.number}}</span>
        <span v-else class="Card__value Card__value--top Card__value__red">{{card.number}}</span>
        <span v-if="card.suit === '♠' || card.suit === '♣' " class="Card__center">{{card.suit}}</span>
        <span v-else class="Card__center__red">{{card.suit}}</span>
        <span v-if="card.suit === '♠' || card.suit === '♣'" class="Card__value Card__value--bottom">{{card.number}}</span>
        <span v-else class="Card__value Card__value--bottom Card__value__red">{{card.number}}</span>
      </div>

      <figure class="Card__pattern" slot="back"></figure>
    </flipper>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
        cards: this.generateCards()
    }
  },
  methods: {
    flipCard(card) {
      card.isFlipped = !card.isFlipped
    },

    shuffle(array) {
      let currentIndex = array.length, temporaryValue, randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      return array;
    },
    generateCards() {
      const suits = ['♠', '❤', '♣', '♦️']
      const numbers = ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K']
      let result = []

      for (let i = 0; i < numbers.length; i++) {
        for (let j = 0; j < suits.length; j++) {
          result.push({
            number: numbers[i],
            suit: suits[j],
            isFlipped: true,
          })
        }
      }
      this.shuffle(result)
      return result
    }
  }
}
</script>

<style>
html,
body{
  height: 100%;
}

body{
  display: flex;
  align-items: center;
  justify-content: center;
}

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
</style>

<style>

  .Card {
    margin-bottom: 20px;
  }

  .Card__face, .Card__pattern {
    width: 80%;
    height: 100%;
    border-radius: 20px;
    box-shadow: 0px 0px 10px 1px #b8b8b7e0;
    /* border: 1px solid rgb(146, 146, 146); */
    cursor: pointer;
  }

  .Card__pattern {
    background-image: url("https://i.imgur.com/cRr1UpB.png");
    background-repeat: no-repeat;
    background-position: center;
    background-size: 50%;
  }

  .Card__face {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
    padding: 15px;
  }

  .Card__value {
    display: block;
    font-size: 18pt;
  }

  .Card__value__red {
    display: block;
    font-size: 18pt;
    color: red;
  }

  .Card__value--top {
    align-self: flex-start;
  }

  .Card__value--bottom {
    align-self: flex-end;
  }

  .Card__center {
    display: block;
    font-size: 32pt;
    align-self: center;
  }

  .Card__center__red {
    display: block;
    font-size: 32pt;
    align-self: center;
    color: red;
  }
</style>

