<template>
  <div id="app">
    <img class="logo" src="./assets/logo.png">
    <hello></hello>
    <p>
      Welcome to Vue-emoji, please use dev-tools to watch the emoji-word that you choose!
    </p>
    <button class="openEmoji" @click="showEmoji = true">Show Emoji</button>
    <emoji :show.sync="showEmoji" :word.sync="wordEmoji"></emoji>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Emoji from './components/Emoji/'

export default {
  components: {
    Hello,
    Emoji
  },
  watch: {
    wordEmoji () {
      console.log(this.wordEmoji) // 获取选中的emoji_word(已转化)
    }
  },
  data () {
    return {
      showEmoji: false,
      wordEmoji: ''
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

button {
  padding: 5px;
  margin-bottom: 10px;
}

ul, li {
  margin: 0;
  padding: 0;
}

ul li {
  list-style: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
