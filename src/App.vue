<template>
  <div class="app">
    <div class="container">
      <div class="app__title">
        Qtion<br>
        kalabloki
      </div>

      <div
        v-for="message in messages"
        :key="message.id"
      >
        {{ message.id }}
        {{ message.author }}
        {{ message.name }}
        {{ message.message }}
      </div>
    </div>
  </div>
</template>

<script>
import messages from './qtion-kalabloki.json';

export default {
  name: 'App',
  data() {
    return {
      messages,
    }
  },
}
</script>

<style lang="scss">
@import "styles/definitions";

.app {
  margin: r(32) 0;

  @include breakpoint(S) {
    margin: r(64) 0;
  }
}

.app__title {
  font-size: r(64);
  font-weight: 100;
  margin-bottom: r(32);

  @include breakpoint(S) {
    font-size: r(80);
  }
}
</style>
