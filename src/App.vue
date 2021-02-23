<template>
  <div class="app">
    <div class="container">
      <div class="app__title">
        Qtion
        <br>
        kalabloki
      </div>

      <Message
        v-for="message in messages"
        :key="message.id"
        :message="message.message"
        :author="message.author"
        :time="message.time"
        class="app__message"
      />
    </div>
  </div>
</template>

<script>
import messages from '@/qtion-kalabloki.json';
import Message from '@/components/Message';

const tags = {
  img: (size, url) => size
    ? `<img src="${url}">`
    : `<img src="${url}" width="${size}">`,
  quote: (sourceId, body) => {
    const sourceMessage = messages.find((message) => message.id === parseInt(sourceId));
    console.log(sourceId)
    console.log(messages);
    return `<figure><figcaption>${sourceMessage.author}</figcaption><blockquote>${body}</blockquote></figure>`;
  },
  url: (url, body) => `<a href="${url}">${body}</a>`,
}

const messagesParsed = messages.map((objMessage) => {
  const tagsOr = Object.keys(tags).join('|');
  const regex = new RegExp(`\\[(${tagsOr})=?(.*?)](.*?)\\[\\/\\1]`, 'gs');
  return {
    ...objMessage,
    message: objMessage.message.replaceAll(regex, (match, tag, ...args) => tags[tag](...args)),
  }
})

export default {
  name: 'App',
  components: {
    Message,
  },
  data() {
    return {
      messages: messagesParsed,
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
  margin-bottom: r(32);
  font-size: r(64);
  font-weight: 700;

  @include breakpoint(S) {
    margin-bottom: r(64);
    font-size: r(80);
  }
}

.app__message {
  & + & {
    margin-top: r(24);

    @include breakpoint(S) {
      margin-top: r(40);
    }
  }
}
</style>
