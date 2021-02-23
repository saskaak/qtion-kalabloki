<template>
  <div class="message">
    <div class="message__meta">
      <div class="message__author">{{ author }}</div>
      <div class="message__time">{{ time }}</div>
    </div>
    <div
      class="message__message"
      v-html="message"
    />
  </div>
</template>

<script>
export default {
  name: 'App',
  props: {
    author: String,
    message: String,
    time: String,
  },
}
</script>

<style lang="scss">
@import "~@/styles/definitions";

.message {
  padding: r(24);
  background-color: #FAFAFA;

  @include breakpoint(SM) {
    padding: r(48);
    font-size: r(18);
  }
}

.message__meta {
  display: flex;
  justify-content: space-between;
  margin-bottom: r(16);
}

.message__author {
  font-weight: 700;
}

.message__time {
  font-size: r(12);
  color: #AAAAAA;
}

.message__message {
  white-space: pre-line;
  line-height: 1.65;

  figure {
    font-size: r(12);
    padding-left: r(8);
    border-left: r(1) solid $color-black;
  }

  figcaption {
    font-weight: 700;
  }

  img {
    max-width: 100%;
  }
}
</style>
