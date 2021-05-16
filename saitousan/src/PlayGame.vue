<template>
  <div>
    <h1>神経衰弱画面</h1>
    <span v-for="(card, index) in cards" :key="index">
      <ul>
        <li v-on:click="open(index)" id="playarea">
          <div v-if="card.isOpen" class="value">{{ card.cardInfo.front }}</div>
          <img
            v-if="!card.isOpen"
            v-bind:src="card.cardInfo.back"
            alt=""
            width="22"
            height="27"
          />
        </li>
      </ul>
    </span>
    <p>最下部</p>
  </div>
</template>


<script>
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
      this.cards[index].isOpen = !this.cards[index].isOpen;
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
  width: 30px;
  height: 50px;
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
}
</style>
