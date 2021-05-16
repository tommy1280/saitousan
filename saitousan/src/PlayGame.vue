<template>
  <div>
    <h1>神経衰弱</h1>
    <span class="card_list" v-for="(card, index) in cards" :key="index">
      <ul>
        <li v-on:click="open(index)" id="playarea">
          <div v-if="card.isOpen" class="value">{{ card.cardInfo.front }}</div>
          <img
            v-if="!card.isOpen"
            v-bind:src="card.cardInfo.back"
            alt=""
            width="44"
            height="54"
          />
        </li>
      </ul>
    </span>
    <p>最下部</p>
  </div>
</template>


<script>
let openCountByPlayer = 0;
export default {
  name: "PlayGame",
  data: function () {
    return {
      cards: [],
      value_cards: [1, 2, 3, 4, 5, 6, 7],
    };
  },
  methods: {
    setCardImage: function () {
      this.pre_cards = this.value_cards.concat(this.value_cards);
      for (let i = 1; i < 15; i++) {
        let card = {
          isOpen: false,
          cardInfo: {
            //カードの表裏
            front: this.pre_cards[i - 1],
            back: require("./assets/logo.png"),
            //正解状況
            isGot: null,
          },
        };
        this.cards.push(card);
      }
    },
    //Fisher-Yates shuffleにより要素をランダムにシャッフルする
    shuffle: function () {
      for (var i = this.cards.length - 1; i > 0; i--) {
        var j = Math.floor(Math.random() * (i + 1));
        var tmp = this.cards[i];
        this.cards[i] = this.cards[j];
        this.cards[j] = tmp;
      }
    },
    open: function (index) {
      if (openCountByPlayer + 1 > 2) return;
      this.cards[index].isOpen = true;
      openCountByPlayer++;

      if (openCountByPlayer == 2) {
        this.isMatched();
        //不一致の場合に元の状態に戻す
        this.reset();
        //一致したら、表向きのままにする
      }
    },
    isMatched: function () {
      let openCards = [];
      this.cards.forEach((card, index) => {
        if (card.isOpen && card.isGot == null) {
          openCards.push({ card, index });
        }
      });

      //値が一致している場合の情報を取得
      let firstCard = openCards[0];
      let secondCard = openCards[1];
      if (firstCard.card.cardInfo.front == secondCard.card.cardInfo.front) {
        this.cards[firstCard.index].isGot = true;
        this.cards[secondCard.index].isGot = true;
      }
    },
    reset: function () {
      setTimeout(() => {
        this.cards.forEach((card, index) => {
          if (card.isOpen && card.isGot == null) {
            this.cards[index].isOpen = false;
          }
        });
        openCountByPlayer = 0;
      }, 2500);
    },
  },
  created() {
    this.setCardImage();
    this.shuffle();
  },
};
</script>

<style>
#playarea {
  float: left;
  margin: 5px;
  width: 60px;
  height: 100px;
  border: dashed 1px;
  cursor: poin;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: arial black;
  color: blue;
  background-color: #efefef;
}

.value {
  color: red;
  font-size: 40px;
}

.card_list {
  text-align: center;
}
</style>
