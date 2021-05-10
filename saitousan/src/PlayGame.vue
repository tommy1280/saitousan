<template>
  <div>
    <h1>神経衰弱画面</h1>
    <span v-for="(card, index) in push_cards" :key="index">
      <ul>
        <li id="playarea" v-bind:src="card">{{ card }}</li>
      </ul>
    </span>
  </div>
</template>


<script>
export default {
  name: "PlayGame",
  data: function () {
    return {
      cards: [],
      push_cards: [1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6, 6, 7, 7],
    };
  },
  methods: {
    setCardImage: function (type) {
      for (let i = 1; i < 14; i++) {
        //let number = ("00" + i).slice(-2);
        let push_value = push_cards[i - 1];
        this.cards.push(push_value);
      }
    },
  },
  mounted() {
    this.setCardImage();
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
}
</style>
