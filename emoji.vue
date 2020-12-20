<template>
  <i class="emoji" ref="font">
    <img v-if="!isMs()" :src="`/emoji/120/${i || text}.png`" :style="{ width: 'auto', height: size }" />
    <span v-else>{{emoji || e}}</span>
  </i>
</template>

<script>
import { emoji2text, text2emoji } from './emojiMap';

export default {
  props: ['i', 'e'],
  data() {
    return {
      size: '1rem',
    };
  },
  computed: {
    emoji() {
      return text2emoji[this.i];
    },
    text() {
      return emoji2text[this.e];
    },
  },
  methods: {
    isMs() {
      const agent = window.navigator.userAgent.toLowerCase();
      return (
        agent.indexOf("win32") >= 0 || agent.indexOf("wow32") >= 0 ||
        agent.indexOf("win64") >= 0 || agent.indexOf("wow64") >= 0
      );
    },
  },
  mounted() {
    const height = window.getComputedStyle(this.$refs.font).fontSize;
    this.size = parseFloat(height) * 1.1 + 'px';
  },
}
</script>

<style lang="scss">
.emoji {
  font-style: normal;
  
  img {
    vertical-align: text-bottom;
  }
}
</style>