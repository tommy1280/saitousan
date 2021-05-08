<template>
  <div>
    <p>{{ title }}</p>
    <p>{{ messages }}</p>
    <p>見えているかな？</p>
    <button v-on:click="incrementCounter">押してね</button>
    <p>{{ counter }}</p>
  </div>
</template>

<script>
export default {
  name: "HelloChild",
  data: function () {
    return {
      title: "ハロー子供",
      counter: 0,
      messages: "メッセージだよ",
    };
  },
  methods: {
    incrementCounter: function () {
      this.counter += 1;
      this.$emit("increment");
      //親コンポーネントに渡して、親側のメソッドをイベントハンドラで動かす
    },
  },
  props: ["message"],
};
</script>
