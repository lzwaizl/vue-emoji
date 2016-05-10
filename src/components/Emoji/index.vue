<style lang="scss">
  @import './index';
</style>

<template>
  <div class="module-emoji" v-if="show">
    <ul class="emoji-tab-list">
      <li class="emoji-item" :class="{'active': curEmojiIndex === $index }" v-for="tab in emojiTabList" @click="switchEmojiTab($key, $index)">{{ tab }}</li>
    </ul>
    <ul class="emoji-data-list">
      <li class="emoji-item" v-for="item in curEmojiList" v-html="item.html" track-by="$index" @click="chooseEmoji(item.word)"></li>
    </ul>
  </div>
</template>

<script>
  import Emoji from './emoji'
  import emojiData from './emoji-data'
  import collection from 'lodash/collection'

  export default {
    props: {
      show: {
        type: Boolean,
        required: true,
        twoWay: true,
        default: false
      },
      word: {
        type: String,
        twoWay: true
      }
    },

    data () {
      return {
        emojiImg: '//7xrnqf.dl1.z0.glb.clouddn.com/img/sheet_apple_64.png',
        emoji: null,
        emojiDataGrouped: null,
        curEmojiIndex: 0,
        curEmojiList: [],
        emojiTabList: {
          People: '人物',
          Nature: '自然',
          Foods: '食物',
          Activity: '活动',
          Places: '地点',
          Objects: '物体',
          Symbols: '符号',
          Flags: '旗帜'
        }
      }
    },
    ready () {
      this._init().switchEmojiTab('People', 0)
    },
    methods: {
      _init () {
        this.emoji = new Emoji()
        this.emoji.use_sheet = true
        this.emoji.img_sets.apple.sheet = this.emojiImg
        this.emojiDataGrouped = collection.groupBy(emojiData, 'c')
        return this
      },

      switchEmojiTab (key, index) {
        this.curEmojiList = []
        this.curEmojiIndex = index
        collection.forEach(this.emojiDataGrouped[key], (value) => {
          let word = `:${value.s}:`
          this.curEmojiList.push({
            word: word,
            html: this.emoji.replace_colons(word)
          })
        })
      },

      chooseEmoji (word) {
        this.word = this.emoji.replace_colons_ex(word)
      }
    }
  }
</script>